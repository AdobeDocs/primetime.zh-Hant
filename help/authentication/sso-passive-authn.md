---
title: 通過被動身份驗證實現SSO
description: 通過被動身份驗證實現SSO
exl-id: ce45899f-6e94-4bb0-a2c1-51f03bd66d8d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# 通過被動身份驗證實現SSO

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 導言

本文檔的範圍是介紹被動身份驗證流的實施以及它如何與我們標準的單點登錄方法配合工作。

## 用酶

Adobe Primetime身份驗證可在應用/站點之間啟用單一登錄(SSO)。 用戶使用其MVPD憑據登錄後，Adobe Primetime驗證將生成一個表示MVPD驗證會話的安全令牌，並使用設備ID將該令牌綁定到用戶設備。 Adobe Primetime驗證將令牌/設備ID儲存在伺服器或設備上。

只要令牌仍然有效，用戶將直接顯示為已驗證。 這樣，用戶在確保交易安全的同時可以更少地輸入其憑據。



此處詳述的業務使用案例有一個非常具體的要求：必須至少對每個訪問的站點對用戶進行一次身份驗證。 這使MVPD能夠應用與authN會話關聯的業務規則，這些業務規則可能因網路而異。 它與當前的TVE承諾相衝突，即用戶只需登錄一次，就可以在屬於Adobe Primetime認證生態系統的所有站點上進行認證。



為了維護業務規則，同時保持良好的用戶體驗，MVPD不要求用戶手動提供憑據資訊。 我們可以從先前設定的會話cookie中獲益，並嘗試使用被動流進行自動重新驗證；從用戶角度看，他將顯示為自動登錄。



為瞭解決這些問題，我們實施了兩個獨特的功能：每個網路的身份驗證和被動身份驗證支援。 MVPD將支援SAML被動authN，在該SAML被動authN中，如果IdP上存在authN會話，則它們只需重新驗證用戶身份，而不管該會話是在哪個站點上建立的。



## 每個網路的身份驗證

此功能可確保MVPD對每個訪問的站點接收一次驗證請求。 此功能意味著Adobe Primetime認證驗證令牌將綁定到請求者ID，因此僅對請求該令牌的網路有效。 因此，一旦用戶在站點&quot;A&quot;上驗證，然後訪問站點&quot;B&quot;，就需要進行驗證。



請注意，由於用戶在MVPD IdP上已經經過身份驗證，因此不需要他提供登錄資訊，而是只需將瀏覽器從站點&quot;B&quot;重定向到MVPD IdP，然後返回。 如果返回，同一用戶仍將在站點「A」上進行身份驗證。



以下流描述了基本的「每網路驗證」功能：





## 被動身份驗證

這樣做的目的是使重新驗證過程在後台進行，而不需要完全瀏覽器重定向和顯示選取器。 結果，從站點A移動到站點B的用戶將自動被認證。



從UX的角度看，此流與使用常規MVPD執行的流之間沒有差別。 用戶看到，在由於訪問站點A而輸入憑據後，將在站點B上自動對其進行身份驗證。



為了使此流可行，MVPD需要支援被動身份驗證，以便在MVPD不再有會話的情況下，隱藏的iframe不會在登錄頁上「卡住」。 這是通過標準「isPassive」屬性完成的。



下圖描述了改進的流和「幕後」被動身份驗證：





SAML請求示例下面是被動authN流的SAML請求示例：


```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
```

業務規則MVPD具有特定的SSO作用域域限制。 例如，某些MVPD（同一媒體公司的SSO，但不跨公司）只能允許某些域。
某些MVPD可能需要實施不同的身份驗證規則。 例如，MVPD可能具有不同的驗證TTL。 此外，MVPD可能會為某些網路啟用基於家庭的身份驗證，而不是為其他網路啟用身份驗證（此處強烈表示家長控制使用案例）。


這些業務要求應牢記，主要使用情形是，在成功使用其MVPD登錄後，不應要求用戶重新登錄。

這可以通過使用帶有被動authN標誌的每個網路的身份驗證來實現。



iOS的已知限制 — 由於iOS本地儲存的性質，SSO流在iOS不適用於由不同供應商開發的應用程式。 有關iOS8及更高版本的SSO的詳細資訊，請參閱本技術說明。


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->
