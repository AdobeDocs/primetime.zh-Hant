---
title: 服務提供者範圍
description: 服務提供者範圍
exl-id: 730c43e1-46c0-4eec-b562-b1ad93cce6d3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 服務提供者範圍 {#service-provoider-scoping}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 概觀 {#overview}

Adobe Primetime驗證與MVPD整合的預設實作是根據 **OLCA規格**. OLCA規格（6.5，主體識別碼）的「驗證需求」區段指出，您可以指出服務提供者(SP)的「主體」識別碼範圍。 （主體識別碼是MVPD傳回SP的模糊化使用者ID。）  在Adobe Primetime驗證整合中，需要MVPD啟用SP驗證請求的範圍設定。

由於Adobe Primetime驗證扮演了程式設計師的SP角色，因此必須實作自訂，以啟用驗證請求的SP範圍設定。  必須這樣做，MVPD才能識別傳遞給MVPD的身分提供者(IdP)的SAML宣告中的網路品牌。  範圍設定可透過下一節所述的兩種方式之一來實作。

## 服務提供者範圍 {#service-provider-scoping}

Adobe Primetime驗證支援以下兩種方式來啟用驗證請求的SP範圍設定：

* **SAML簽發者方法。**  在此方法中，「請求者ID」會附加至SAML驗證請求中的SAML簽發者字串。

* **自訂範圍設定屬性方法。**  在此方法中，「請求者ID」會明確包含在SAML驗證請求中，作為自訂「範圍設定」屬性。

>[!NOTE]
>
>「請求者ID」是Adobe Primetime驗證提及程式設計師網路品牌的方式（例如：「CNN」是Turner網路的品牌之一）。

### SAML簽發者方法 {#saml-issuer-approach}

此方法使用SAML `<Issuer>` 元素，如下列代碼片段所示：

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 自訂範圍設定屬性方法 {#custom-scoping-property-approach}

此方法會使用名為「Scoping」的自訂屬性，如以下SAML驗證請求程式碼片段所示：

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->
