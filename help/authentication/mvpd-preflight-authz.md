---
title: MVPD預檢授權
description: MVPD預檢授權
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# MVPD預檢授權

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#mvpd-preflight-authz-intro}

「預檢授權」是針對多個資源的輕量型授權檢查。 程式設計師主要使用它來裝飾他們的UI（例如，用鎖和解鎖表徵圖指示訪問狀態）。

Adobe Primetime驗證目前可透過兩種方式支援MVPD的預檢授權，方法為透過AuthN回應屬性或多頻道AuthZ請求。  以下情況說明了實施預檢授權的不同方法的成本/優勢：

* **最佳案例情境** - MVPD會在授權階段（多通道AuthZ）提供預先授權資源的清單。
* **最壞情況**  — 如果MVPD不支援任何形式的多資源授權，Adobe Primetime驗證伺服器會針對資源清單中的每個資源執行對MVPD的授權呼叫。 此情境對預檢授權請求的回應時間具有影響（與資源數量成比例）。 它可增加Adobe和MVPD伺服器上造成效能問題的負載。 此外，它會產生授權要求/回應事件，而不需要實際播放。
* **已棄用** - MVPD會在驗證階段提供預先授權資源的清單，因此不需要網路呼叫，甚至不需要預檢請求，因為清單是在用戶端快取的。

雖然MVPD不必支援預檢授權，但以下幾節將說明Adobe Primetime驗證可支援的預檢授權方法，然後再回復到上述最壞的情況。

## 驗證中的預檢 {#preflight-authn}

此預檢方案與OLCA相容（電纜）。 7.5.2節中的「驗證和授權介面1.0規範」標題為「驗證斷言內的屬性陳述式」，說明SAML驗證回應如何包含預先授權的資源清單。 如果IdP支援此功能，Adobe Primetime驗證伺服器將能在驗證時產生預先設定的資源清單，並連同驗證Token一起在用戶端上快取。 此方法還實現了最佳情況，並且當程式設計師調用checkPreauthorizedResources()時，不會執行任何網路調用，因為客戶端上已有所有內容。

### SAML屬性語句中的自定義資源清單 {#custom-res-saml-attr}

IdP的SAML驗證回應應包含AttributeStatement，其中包含AdobePass應授權的資源名稱。  有些MVPD會以下列格式提供此內容：

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

上述範例提供包含兩個預先授權資源的清單：「MMOD」和「2012年奧運會」。

這有效地實現了最佳情況，並且當程式設計師調用checkPreauthorizedResources()時，不會執行網路調用，因為所有內容都已在客戶端上。

## AuthZ中的多通道預檢 {#preflight-multich-authz}

此預檢實施也與OLCA相容(Cablelabs)。  驗證和授權介面1.0規範（第7.5.3節和7.5.4節）描述了使用SAML斷言或XACML從MVPD請求授權資訊的方法。 這是查詢不支援MVPD的MVPD授權狀態的建議方式，作為驗證流程的一部分。 Adobe Primetime驗證會向MVPD發出單一網路呼叫，以擷取授權資源清單。


Adobe Primetime驗證從程式設計師應用程式接收資源清單。 Adobe Primetime驗證的MVPD整合接著可以進行一個包含所有這些資源的AuthZ呼叫，然後剖析回應並擷取多個允許/拒絕決策。  使用多通道AuthZ情況進行預檢的流程如下：

1. 程式設計師的應用程式通過預檢客戶端API發送以逗號分隔的資源清單，例如：&quot;TestChannel1,TestChannel2,TestChannel3&quot;。
1. MVPD預檢AuthZ請求呼叫包含多個資源，且具有下列結構：

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

有些MVPD的授權端點支援在一個請求中對多個資源進行授權，但不符合多通道AuthZ中所述的案例。 這些特定MVPD需要自訂工作。

Adobe也可支援多通道授權，而不需變更現有實作。  Adobe和MVPD技術小組之間需要審查此方法，以確保其如預期般運作。

## 支援預檢授權的MVPD {#mvpds-supp-preflight-authz}

下表列出支援預檢授權的MVPD，以及支援的預檢類型和已知限制：

| 飛行前進 | MVPD | 附註 |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| 多通道AuthZ | Comcast AT&amp;T代理Clearleap Charter_Direct代理GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| 使用者中繼資料中的管道陣列 | HTC突然連結 | 所有Syncor直接整合也可支援此方法。 |
| 分支並連接 | 上面未列出的所有其他 | 預設的已檢查資源數上限= 5。 |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
