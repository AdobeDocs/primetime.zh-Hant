---
title: MVPD預檢授權
description: MVPD預檢授權
exl-id: da2e7150-b6a8-42f3-9930-4bc846c7eee9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# MVPD預檢授權

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#mvpd-preflight-authz-intro}

「預檢授權」是對多個資源的輕量授權檢查。 程式設計師主要使用它來裝飾他們的UI （例如，使用鎖定和解鎖圖示來指示存取狀態）。

Adobe Primetime驗證目前可透過兩種方式為MVPD支援預檢授權，即透過AuthN回應屬性或透過多通道AuthZ請求。  下列案例說明您可以實作預檢授權的不同方式的成本/效益：

* **最佳案例** - MVPD會提供授權階段期間預先授權的資源清單（多通道驗證）。
* **最壞情況**  — 如果MVPD不支援任何形式的多重資源授權，Adobe Primetime驗證伺服器會針對資源清單中的每個資源對MVPD執行授權呼叫。 此情境會影響（與資源數量成比例）預檢授權請求的回應時間。 這可能會增加Adobe和MVPD伺服器上的負載，造成效能問題。 此外，它也會產生授權請求/回應事件，而不需要實際播放。
* **已棄用** - MVPD會在驗證階段提供預先授權的資源清單，因此不需要網路呼叫，甚至不需要預檢要求，因為清單會在使用者端上快取。

雖然MVPD不需要支援預檢授權，但以下幾節會說明Adobe Primetime驗證在回覆至上述最壞情況之前，可以支援的一些預檢授權方法。

## 在AuthN中預檢 {#preflight-authn}

此預檢情況與OLCA相容(Cableabs)。 驗證與授權介面1.0規格小節7.5.2標題為「驗證判斷提示內的屬性陳述式」，說明SAML驗證回應如何包含預先授權的資源清單。 如果IdP支援此功能，Adobe Primetime驗證伺服器就可以在驗證時產生預先定義的資源清單，並和驗證Token一起快取該清單在使用者端上。 此方法也可達到最佳案例，而且程式設計師呼叫checkPreauthorizedResources()時不會執行任何網路呼叫，因為所有專案都已在使用者端上。

### SAML屬性陳述式中的自訂資源清單 {#custom-res-saml-attr}

IdP的SAML驗證回應應包含包含AdobePass應授權的資源名稱的AttributeStatement。  有些MVPD會以下列格式提供此內容：

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

上述範例提供包含兩個預先授權資源的清單：「MMOD」和「Oppornimum2012」。

這實際上實現了最佳案例，並且程式設計師呼叫checkPreauthorizedResources()時不會執行任何網路呼叫，因為所有內容都已在使用者端上。

## AuthZ中的多頻道預檢 {#preflight-multich-authz}

此預檢實作也與OLCA相容(Cablelabs)。  驗證與授權介面1.0規格（第7.5.3節和第7.5.4節）說明使用SAML宣告或XACML向MVPD請求授權資訊的方法。 對於不支援此驗證流程的MVPD，建議使用此方式查詢授權狀態。 Adobe Primetime驗證會向MVPD發出單一網路呼叫，以擷取授權資源的清單。


Adobe Primetime驗證會從程式設計師的應用程式接收資源清單。 Adobe Primetime驗證的MVPD整合接著可以執行一個AuthZ呼叫（包含所有這些資源），然後剖析回應並擷取多個允許/拒絕決定。  使用多管道AuthZ案例的預檢流程運作方式如下：

1. 程式設計師的應用程式會透過預檢使用者端API傳送逗號分隔的資源清單，例如：「TestChannel1，TestChannel2，TestChannel3」。
1. MVPD預檢AuthZ要求呼叫包含多個資源，並具有下列結構：

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

## 多個資源的自訂授權 {#custom-authz}

某些MVPD具有授權端點，這些端點支援在一個請求中對多個資源進行授權，但它們不屬於多通道AuthZ中所述的情境。 這些特定的MVPD需要自訂工作。

Adobe也可以支援多管道授權，而不需變更現有實作。  此方法需要在Adobe和MVPD技術團隊之間審查，以確保它按預期運作。

## 支援預檢授權的MVPD {#mvpds-supp-preflight-authz}

下表列出支援「預檢授權」的MVPD，及其支援的預檢型別和已知限制：

| 預檢方法 | MVPD | 附註 |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| 多通道AuthZ | Comcast AT&amp;T Proxy Clearleap Charter_Direct Proxy GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| 使用者中繼資料中的頻道組合 | Suddenlink HTC | 所有Synacor直接整合也可以支援此方法。 |
| 取用並加入 | 以上未列出的所有其他專案 | 已核取的預設最大資源數= 5。 |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
