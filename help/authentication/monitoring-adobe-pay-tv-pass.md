---
title: 監控Adobe Primetime驗證
description: 監控Adobe Primetime驗證
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 監控Adobe Primetime驗證 {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#intro}

客戶可使用 [納吉奧](http://www.nagios.org) 或其他工具來檢查Adobe Primetime驗證是否啟動或關閉。 

## 監控端點 {#monitoring-endpoints}

### 可監視的端點 {#endpoints-to-monitor}

* 所有平台的配置端點： `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]` — 可透過HTTP或HTTPS取得（視內容提供者的開發人員所做的選擇而定）。 如果此端點遺失，表示您的內容將無法用於所有平台和所有MVPD。 對於無用戶端REST API，我們還提供下列端點：  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* 下列端點是Adobe Primetime驗證Web SDK的一部分。  如果缺少它，表示所有程式設計師和所有Web屬性的付費電視傳遞被關閉：

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### 不應監視的端點 {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   您一律會收到503錯誤，因為此端點需要MVPD SAML回應。

* 其他權限端點 —  `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

您無法監視這些端點，因為它們需要相關回覆的裝載。
