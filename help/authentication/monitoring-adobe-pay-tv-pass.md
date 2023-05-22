---
title: 監視Adobe Primetime身份驗證
description: 監視Adobe Primetime身份驗證
exl-id: fb000e9d-b5aa-45b1-a914-9e419ec8a4d9
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 監視Adobe Primetime身份驗證 {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#intro}

客戶可以 [納吉奧](http://www.nagios.org) 或其他工具來檢查Adobe Primetime驗證是啟動還是關閉。 

## 監視終結點 {#monitoring-endpoints}

### 可監視的端點 {#endpoints-to-monitor}

* 所有平台的配置終結點： `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]` — 它可通過HTTP或HTTPS（取決於內容提供商的開發人員所做的選擇）使用。 如果缺少此終結點，則表示您的內容不會跨所有平台和所有MVPD可用。 對於無客戶端REST API，我們還有以下端點：  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`。

* 以下端點是Adobe Primetime驗證Web SDK的一部分。  如果缺少，則表示所有程式設計師和所有Web屬性都將使用pay-TVpass:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`

 
### 不應監視的終結點 {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

   您總會遇到503錯誤，因為此終結點需要MVPD SAML響應。

* 其他權利終結點 —  `adobe-services/1.0/authenticate/`。 `adobe-services/1.0/deviceShortAuthorize`。 `adobe-services/1.0/authorize`

無法監視這些端點，因為它們需要相關答復的負載。
