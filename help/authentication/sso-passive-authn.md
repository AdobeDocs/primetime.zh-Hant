---
title: 通過被動身份驗證的SSO
description: 通過被動身份驗證的SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 通過被動身份驗證的SSO

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 簡介

本檔案的範圍是說明被動式驗證流程的實作，以及這如何與我們標準的單一登入方法搭配運作。

## 使用案例

Adobe Primetime驗證可在應用程式/網站之間啟用單一登入(SSO)。 使用者以其MVPD憑證登入後，Adobe Primetime驗證會產生代表MVPD驗證工作階段的安全Token，並使用裝置ID將該Token系結至使用者裝置。 Adobe Primetime驗證會將Token /裝置ID儲存在伺服器或裝置上。

只要Token仍有效，使用者就會直接顯示為已驗證。 這可讓使用者更少輸入憑證，同時確保交易安全。



以下詳述的業務使用案例是一項非常具體的要求：必須至少對每個造訪的網站驗證一次使用者。 這可讓MVPD套用與authN工作階段相關聯的業務規則，該工作階段可能因網路而異。 與目前TVE的承諾相衝突，使用者只需登入一次，即可在屬於Adobe Primetime驗證生態系統的所有網站上驗證。



為了維護業務規則並保持良好的用戶體驗，MVPD「不」要求用戶手動提供憑據資訊。 我們可以從先前設定的工作階段Cookie中獲益，並嘗試使用被動式流程自動重新驗證；從使用者的角度來看，他會自動顯示為已登入。



為了解決這些問題，我們實作了2個不同的功能：每個網路的身份驗證和被動身份驗證支援。 MVPD將支援SAML被動authN，無論在哪個網站建立該工作階段，只要IdP上存在authN工作階段，MVPD就會重新驗證使用者。



## 每個網路的身份驗證

此功能可確保MVPD收到每個已造訪網站一次的驗證請求。 此功能表示Adobe Primetime驗證驗證Token將限制至requestorID，因此僅對請求Token的網路有效。 因此，當使用者在網站「A」上進行驗證，之後又瀏覽網站「B」時，就需要進行驗證。



請注意，由於使用者已在MVPD IdP上通過驗證，因此系統不會要求他提供登入資訊，而是只會將瀏覽器從網站&quot;B&quot;重新導向至MVPD IdP，然後返回。 如果同一位使用者返回，仍會在網站「A」上驗證。



以下流描述了每個網路的基本身份驗證功能：





## 被動驗證

其目標是讓重新驗證程式在背景執行，而不需要完全的瀏覽器重新導向且不會顯示選擇器。 因此，從網站A移至網站B的使用者將會自動進行驗證。



從UX的觀點來看，此流量與以一般MVPD執行的流量之間沒有差異。 使用者看到的是，在因瀏覽網站A而輸入認證後，就會在網站B自動進行驗證。



為了讓此流程可行，MVPD將需要支援被動式驗證，這樣在MVPD不再有工作階段的情況下，隱藏的iframe就不會「卡住」在登入頁面上。 這是透過標準「isPassive」屬性來完成。



下圖說明改進的流程和「幕後」被動驗證：





SAML要求範例以下是被動authN流程的SAML要求範例：


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

業務規則MVPD具有特定的SSO範圍域限制。 例如，某些MVPD（相同媒體公司的SSO，但不跨公司）只能允許某些網域。
某些MVPD可能需要執行不同的驗證規則。 例如，MVPD的每個不同網路可能具有不同的驗證TTL。 此外，MVPD可能會為某些網路啟用基於家庭的驗證，但不會為其他網路啟用（此處強烈顯示家長控制使用案例）。


這些業務需求應記住，主要使用案例是，使用者在成功透過MVPD登入後，不應需要再次登入。

這可以通過使用具有被動authN標誌的每個網路的身份驗證來實現。



iOS的已知限制 — 由於iOS本機儲存的性質，不同廠商所開發的應用程式的SSO流程在iOS上無法運作。 有關iOS 8及更新版本中SSO的詳細資訊，請參閱本技術說明。


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->