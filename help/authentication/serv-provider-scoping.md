---
title: 服務提供商範圍
description: 服務提供商範圍
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 服務提供商範圍 {#service-provoider-scoping}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

與MVPD的Adobe Primetime驗證整合的預設實作是以 **OLCA規範**. OLCA規範（6.5，主體標識符）的「驗證要求」部分說明，可以指明服務提供商(SP)對主體標識符的範圍。 （主旨識別碼是MVPD傳回SP的模糊化使用者ID。）  在Adobe Primetime驗證整合中，需要MVPD啟用SP驗證請求的範圍界定。

由於Adobe Primetime身份驗證承擔了程式設計師的SP角色，因此必須實施一個定製，以允許SP對身份驗證請求進行範圍界定。  這必須完成，MVPD才能識別在SAML斷言中傳遞至MVPD的身分提供者(IdP)的網路品牌。  範圍劃分可透過下一節所述的兩種方式之一實施。

## 服務提供商範圍 {#service-provider-scoping}

Adobe Primetime驗證支援下列兩種方式，以啟用驗證請求的SP範圍劃分：

* **SAML頒發者方法。**  在此方法中，「請求者ID」會附加至SAML驗證請求中的SAML核發者字串。

* **自訂範圍劃分屬性方法。**  在此方法中，「請求者ID」會明確納入為SAML驗證請求中的自訂「範圍界定」屬性。

>[!NOTE]
>
>「請求者ID」是Adobe Primetime驗證引用程式設計師網路品牌的方式(例如：《CNN》是特納網路的品牌之一。

### SAML頒發者方法 {#saml-issuer-approach}

此方法使用SAML `<Issuer>` 元素，如此程式碼片段所示：

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 自訂範圍劃分屬性方法 {#custom-scoping-property-approach}

此方法使用名為「範圍分析」的自訂屬性，如SAML驗證請求的此片段所示：

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