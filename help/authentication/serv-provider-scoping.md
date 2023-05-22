---
title: 服務提供商範圍界定
description: 服務提供商範圍界定
exl-id: 730c43e1-46c0-4eec-b562-b1ad93cce6d3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 服務提供商範圍界定 {#service-provoider-scoping}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

與MVPD的Adobe Primetime身份驗證整合的預設實現基於 **OLCA規範**。 OLCA規範（6.5，主題標識符）的「驗證要求」部分指出，可以為主題標識符指明服務提供商(SP)的作用域。 （主題標識符是MVPD返回到SP的模糊用戶ID。）  在Adobe Primetime身份驗證整合中，需要MVPD啟用SP身份驗證請求的作用域。

隨著Adobe Primetime身份驗證成為程式設計師的SP角色，必須實施允許身份驗證請求的SP作用域的自定義。  需要執行此操作，以便MVPD可以標識在SAML斷言中傳遞給MVPD的標識提供程式(IdP)的網路品牌。  範圍界定可以採用下一節所述的兩種方式之一來實現。

## 服務提供商範圍界定 {#service-provider-scoping}

Adobe Primetime身份驗證支援以下兩種方法來啟用身份驗證請求的SP作用域：

* **SAML頒發者方法。**  在此方法中，「請求者ID」將附加到SAML驗證請求中的SAML頒發者字串。

* **自定義作用域屬性方法。**  在此方法中， SAML驗證請求中將「請求者ID」顯式地作為自定義「作用域」屬性包含在內。

>[!NOTE]
>
>「請求者ID」是Adobe Primetime驗證如何指代程式設計師的網路品牌(例如：&quot;CNN&quot;是特納電視台的品牌之一)。

### SAML頒發者方法 {#saml-issuer-approach}

此方法使用SAML `<Issuer>` SAML身份驗證請求中的元素，如此代碼段所示：

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 自定義作用域屬性方法 {#custom-scoping-property-approach}

此方法使用名為「作用域」的自定義屬性，如SAML驗證請求的此代碼段所示：

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
