---
title: 監控Adobe Primetime驗證
description: 監控Adobe Primetime驗證
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 監控Adobe Primetime驗證 {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

## 簡介 {#intro}

客戶可以使用 [納吉歐斯](http://www.nagios.org) 或其他工具來檢查Adobe Primetime驗證是否正常運作。

## 監控端點 {#monitoring-endpoints}

### 您可以監視的端點 {#endpoints-to-monitor}

* 所有平台的設定端點： `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]` — 此變數可透過HTTP或HTTPS提供（視內容提供者的開發人員所做的選擇而定）。 如果缺少此端點，表示您的內容將無法在所有平台和所有MVPD上使用。 對於無使用者端REST API，我們還有以下端點：  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* 下列端點是Adobe Primetime驗證Web SDK的一部分。  如果遺漏，則表示所有程式設計師和所有Web屬性的pay-TVpass都會關閉：

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`


### 不應監視的端點 {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

  您一律會收到503錯誤，因為此端點需要有MVPD SAML回應。

* 其他權益端點 —  `adobe-services/1.0/authenticate/`， `adobe-services/1.0/deviceShortAuthorize`， `adobe-services/1.0/authorize`

您無法監視這些端點，因為它們需要相關回覆的裝載。
