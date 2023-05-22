---
title: 通過HTTPS安全廣告載入
description: 通過HTTPS安全廣告載入
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 通過HTTPS安全廣告載入{#secure-ad-loading-over-https}

Adobe Primetime可以通過https請求第三方廣告伺服器，即使播放器位於http上。 只有這些ad-server調用在Auditude Ad解析器階段升級到客戶端尋求的https。

>[!NOTE]
>
>此功能不支援Flash。

使用以下命令啟用安全廣告載入。 預設情況下未啟用它。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
