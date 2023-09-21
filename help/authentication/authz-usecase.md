---
title: MVPD授權
description: MVPD授權
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# MVPD授權

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#mvpd-authz-overview}

授權(AuthZ)是透過Adobe代管的後端伺服器與MVPD AuthZ端點之間的後端通道（伺服器對伺服器）通訊執行。

對於AuthZ請求，授權端點應能夠處理至少以下引數：

* **Uid**. 從驗證步驟收到的使用者ID。

* **資源ID**. 識別指定內容資源的字串。 這個資源ID是由程式設計師指定的，且MVPD必須增強這些資源的商業規則（例如，透過檢查使用者是否已訂閱特定通道）。

除了判斷使用者是否獲得授權外，回應必須包括此授權的存留時間(TTL)，即授權到期時。 如果未設定TTL，AuthZ要求將會失敗。  基於這個原因， **TTL是Adobe Primetime驗證端的強制組態設定**，以涵蓋MVPD未在其要求中包含TTL的情況。

## 授權要求 {#authz-req}

AuthZ要求必須包含代表其提出要求的主體、主體嘗試存取的資源、主體嘗試對資源執行的動作，以及即將執行作業的環境。 在Adobe Primetime驗證的特定情況下，這些元素會對應至：

| XACML元素 | 對應至 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| 主旨 | 由已驗證工作階段所識別的主體，由SAML判斷提示的「subject-token」AttributeValue參照。 |
| 資源 | 受保護資源的URI。 |
| 動作 | 檢視。 |
| 環境 | 包括請求使用者端的IP位址（如SP所見）。 |



此時SP必須準備XACML Authorization DecisionQuery並(透過HTTPPOST)將其傳送到（先前同意的）原則決定點(PDP)以進行IdP。 以下是簡單XACML請求的範例（請參閱XACML核心規格）：

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


在收到AuthZ要求之後，MVPD的PDP會評估要求並決定是否應允許主體在資源上執行要求的動作。 然後MVPD會傳回包含決定、狀態代碼和訊息的回應，如下面的授權回應所述。

## 授權回應 {#authz-response}

對AuthZ要求的回應是在MVPD評估要求並套用要求的商業規則以判斷是否允許主體在資源上執行要求的動作之後作出。 針對Adobe Primetime驗證的傳回回應會再次以XACML核心規格表示，並附上SP作為原則執行點(PEP)的決定、狀態代碼、訊息和義務。 以下是範例回應：

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

以下是Adobe Primetime驗證支援且讓程式設計師能夠履行的DENY義務清單：

* **urn:tve:xacml：2.0:obligations:restrict-pc**  — 訂閱者未通過家長監護檢查，SP必須採取適當措施限制此內容的存取。

* **urn:tve:xacml：2.0:obligations:升級**  — 訂閱者沒有適當的訂閱層級。  必須升級訂閱才能存取內容。

Adobe Primetime驗證支援下列專案 **允許** 讓程式設計師能夠履行這些義務：

* **urn:cablelabs:olca：1.0:obligations:記錄** - Adobe Pass會記錄交易，並可透過議定的報告機制提供。

* **urn:cablelabs:olca：1.0:obligations:重新驗證** - Adobe Primetime驗證會在n秒內重新整理授權（透過XACML AttributeAssignment指定為義務的引數 — 請參閱XACML核心規格，第5.46節）。

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
