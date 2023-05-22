---
title: MVPD授權
description: MVPD授權
exl-id: 215780e4-12b6-4ba6-8377-4d21b63b6975
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# MVPD授權

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#mvpd-authz-overview}

授權(AuthZ)通過承載Adobe的後端伺服器與MVPD AuthZ端點之間的後通道（伺服器到伺服器）通信執行。

對於AuthZ請求，授權終結點應至少能夠處理以下參數：

* **UID**。 從驗證步驟接收的用戶ID。

* **資源ID**。 標識給定內容資源的字串。 此資源ID由程式設計師指定，MVPD必須加強這些資源上的業務規則（例如，檢查用戶是否訂閱了特定渠道）。

除了確定用戶是否已授權外，響應還必須包括此授權的生存時間(TTL)，即授權到期時。 如果未設定TTL，則AuthZ請求將失敗。  因此， **TTL是Adobe Primetime身份驗證端的強制配置設定**，以覆蓋MVPD在其請求中不包含TTL的情況。

## 授權請求 {#authz-req}

AuthZ請求必須包括代表其提出請求的主題、該主題嘗試訪問的資源、該主題嘗試對資源執行的操作以及即將進行操作的環境。 在Adobe Primetime驗證的特定情況下，這些元素對應於：

| XACML元素 | 對應於 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| 主題 | 由已驗證會話標識的主體，由SAML斷言的「subject-token」 AttributeValue引用。 |
| 資源 | 受保護資源的URI。 |
| 操作 | 。 |
| 環境 | 包括請求客戶端的IP地址，如SP所見。 |



此時，SP必須準備XACML授權DecisionQuery並將其(通過HTTPPOST)發送到（先前商定的）策略決策點(PDP)以獲取IdP。 下面是簡單XACML請求的示例（請參見XACML核心規範）:

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


在接收到AuthZ請求後，MVPD的PDP評估該請求並確定是否應允許該對象對資源執行所請求的操作。 然後，MVPD將返回包含「決定」、「狀態」代碼和消息的響應，如下面的「授權響應」中所述。

## 授權響應 {#authz-response}

在MVPD評估請求並應用所請求的業務規則來確定是否允許主體對資源執行所請求的操作之後，對AuthZ請求的響應即出現。 在XACML核心規範後，返回的對Adobe Primetime驗證的響應將再次表示為SP作為策略實施點(PEP)具有的決定、狀態代碼、消息和義務。 以下是示例響應：

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

* **甕:tve:xacml:2.0:obligations:限制**  — 訂閱伺服器未通過家長控制檢查，SP必須採取適當措施限制對此內容的訪問。

* **甕:tve:xacml:2.0:obligations:升級**  — 訂閱伺服器沒有適當的訂閱級別。  必須升級訂閱才能訪問內容。

Adobe Primetime身份驗證支援以下 **許可** 使程式設計師能夠履行這些義務和履行這些義務：

* **甕:cablelabs:olca:1.0:obligations:日誌** -Adobe Pass記錄交易，並可通過商定的報告機制提供。

* **甕:cablelabs:olca:1.0:obligations:重奧茨** -Adobe Primetime驗證在n秒內再次刷新授權（通過XACML AttributeAssignment指定為Oractive的參數 — 請參閱XACML核心規範第5.46節）。

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->
