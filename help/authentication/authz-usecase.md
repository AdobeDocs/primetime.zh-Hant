---
title: MVPD授權
description: MVPD授權
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# MVPD授權

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#mvpd-authz-overview}

授權(AuthZ)是透過Adobe托管後端伺服器與MVPD AuthZ端點之間的後端通道（伺服器對伺服器）通訊來執行。

對於AuthZ請求，授權端點應能至少處理下列參數：

* **Uid**. 從驗證步驟接收的使用者ID。

* **資源ID**. 識別指定內容資源的字串。 此資源ID由程式設計師指定，MVPD必須加強這些資源上的業務規則（例如，通過檢查用戶是否訂閱了某個渠道）。

除了判斷使用者是否獲得授權外，回應還必須包含此授權的存留時間(TTL)，即授權過期的時間。 如果未設定TTL,AuthZ請求將會失敗。  因此， **TTL是Adobe Primetime驗證端的強制設定**，以涵蓋MVPD未在其要求中包含TTL的情況。

## 授權請求 {#authz-req}

AuthZ請求必須包含代表提出請求的主體、主體嘗試存取的資源、主體嘗試對資源執行的動作，以及即將進行操作的環境。 在Adobe Primetime驗證的特定案例中，這些元素對應至：

| XACML元素 | 對應至 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| 主旨 | 由已驗證工作階段所識別的主體，由SAML斷言的「主旨代號」AttributeValue所參照。 |
| 資源 | 受保護資源的URI。 |
| 動作 | 檢視。 |
| 環境 | 包括請求客戶端的IP地址，如SP所示。 |



此時，SP必須準備XACML授權DecisionQuery，並(通過HTTPPOST)將其發送到（先前商定的）策略決策點(PDP)以獲取IdP。 以下是簡單XACML請求的範例（請參閱XACML核心規格）:

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


收到AuthZ請求後，MVPD的PDP會評估請求，並判斷是否應允許主體對資源執行請求的動作。 然後，MVPD會傳回包含決策、狀態碼和訊息的回應，如下方的授權回應所述。

## 授權回應 {#authz-response}

在MVPD評估請求並套用請求的業務規則以判斷是否允許主體對資源執行請求的動作之後，才會回應AuthZ請求。 傳回的對Adobe Primetime驗證的回應會在XACML核心規格後再次表示，其中包含SP作為策略執行點(PEP)具有的Decision、Status代碼、消息和Expility。 以下是範例回應：

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

以下是Adobe Primetime身份驗證支援並使程式設計師能夠履行的DENY義務清單：

* **回歸:tve:xacml:2.0:obligations:restrict-pc**  — 訂閱者未通過家長控制檢查，SP必須採取適當措施限制對此內容的訪問。

* **回歸:tve:xacml:2.0:obligations:升級**  — 訂閱者沒有適當的訂閱級別。  必須升級訂閱才能訪問內容。

Adobe Primetime驗證支援下列 **許可** 使程式設計師能夠履行這些義務：

* **回歸:cablelabs:olca:1.0:obligations:記錄** - Adobe Pass記錄交易，並可透過商定的報告機制提供。

* **回歸:cablelabs:olca:1.0:obligations:re-authz** - Adobe Primetime驗證會在n秒內再次重新整理授權（透過XACML AttributeAssignment指定為Odiction的引數 — 請參閱XACML核心規格，第5.46節）。

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->