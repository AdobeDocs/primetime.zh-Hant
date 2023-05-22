---
title: MVPD印前檢查授權
description: MVPD印前檢查授權
exl-id: da2e7150-b6a8-42f3-9930-4bc846c7eee9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# MVPD印前檢查授權

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#mvpd-preflight-authz-intro}

「印前檢查授權」是針對多個資源的輕量授權檢查。 程式設計師主要使用它來裝飾他們的UI（例如，用鎖定和解鎖表徵圖指示訪問狀態）。

Adobe Primetime驗證目前可以通過兩種方式支援MVPD的印前檢查授權，即通過AuthN響應屬性或通過多通道AuthZ請求。  以下方案描述了您實施印前授權的不同方法的成本/好處：

* **最佳案例方案** - MVPD在授權階段（多通道AuthZ）提供預授權資源清單。
* **最壞情況方案**  — 如果MVPD不支援任何形式的多資源授權，則Adobe Primetime認證伺服器將對資源清單中的每個資源執行對MVPD的授權調用。 此方案對印前檢查授權請求的響應時間具有影響（與資源數成比例）。 它可以增加Adobe和MVPD伺服器上的負載，從而導致效能問題。 另外，它將生成授權請求/響應事件，而不需要實際播放。
* **已棄用** - MVPD在驗證階段提供預授權資源清單，因此不需要網路呼叫，甚至不需要預檢請求，因為清單已快取在客戶端上。

雖然MVPD不必支援飛行前授權，但以下各節描述了Adobe Primetime身份驗證可支援的某些飛行前授權方法，然後又回到上述最壞情況情形。

## AuthN中的預檢 {#preflight-authn}

此印前檢查方案為OLCA相容(Cableabs)。 「驗證和授權介面1.0規範」7.5.2節標題為「驗證斷言中的屬性語句」，介紹SAML驗證響應如何包含預授權資源清單。 如果IdP支援此功能，Adobe Primetime認證伺服器將能夠在認證時生成預配置資源清單，並將其與認證令牌一起快取到客戶端上。 此方法還實現了最佳案例情形，並且當程式設計師調用checkPreauthorizedResources()時，不會執行網路調用，因為客戶端上已有所有內容。

### SAML屬性語句中的自定義資源清單 {#custom-res-saml-attr}

IdP的SAML驗證響應應包含AdobePass應授權的資源名稱的AttributeStatement。  某些MVPD以以下格式提供此功能：

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

上面的示例顯示包含兩個預授權資源的清單：「MMOD」和「2012年奧運會」。

這有效地實現了最佳案例方案，並且當程式設計師調用checkPreauthorizedResources()時不會執行網路調用，因為客戶端上已有所有內容。

## AuthZ中的多通道預檢 {#preflight-multich-authz}

此印前檢查實現也是OLCA相容(Cablelabs)。  驗證和授權介面1.0規範(7.5.3和7.5.4節)介紹了使用SAML斷言或XACML從MVPD請求授權資訊的方法。 這是作為驗證流的一部分查詢不支援此功能的MVPD的授權狀態的推薦方法。 Adobe Primetime驗證向MVPD發出單個網路調用以檢索授權資源清單。


Adobe Primetime驗證從程式設計師應用程式接收資源清單。 Adobe Primetime驗證的MVPD整合可以進行一個包括所有這些資源的AuthZ調用，然後分析響應並提取多個允許/拒絕決定。  使用多通道AuthZ方案進行預檢的流程如下：

1. 程式設計師應用通過印前檢查客戶端API發送以逗號分隔的資源清單，例如：&quot;TestChannel1,TestChannel2,TestChannel3&quot;。
1. MVPD印前檢查AuthZ請求調用包含多個資源，並具有以下結構：

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## 多個資源的自定義授權 {#custom-authz}

某些MVPD具有支援在一個請求中對多個資源進行授權的授權終結點，但它們不屬於多通道AuthZ中描述的情形。 這些特定MVPD需要自定義工作。

Adobe還可以支援多通道授權，而無需更改現有實現。  需要在Adobe和MVPD技術小組之間審查這一辦法，以確保它按預期工作。

## 支援印前檢查授權的MVPD {#mvpds-supp-preflight-authz}

下表列出了支援「印前檢查授權」的MVPD，以及它們支援的印前檢查類型和已知限制：

| 印前檢查方法 | MVPD | 注釋 |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| 多通道AuthZ | Comcast AT&amp;T代理Clearleap Charter_Direct代理GLDS Rogers Verizon OSN Bell Sasktel Optimization AlticeOne |  |
| 用戶元資料中的通道清單 | 突然連結HTC | 所有Synacor直接整合都可支援此方法。 |
| 叉和聯接 | 上面未列出的所有其他內容 | 選中的預設最大資源數= 5。 |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
