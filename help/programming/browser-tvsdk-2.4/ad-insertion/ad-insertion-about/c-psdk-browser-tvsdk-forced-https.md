---
title: 安全透過HTTPS載入廣告
description: 安全透過HTTPS載入廣告
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 安全透過HTTPS載入廣告{#secure-ad-loading-over-https}

即使播放器託管於http，Adobe Primetime仍可透過https要求協力廠商廣告伺服器。 只有這些廣告伺服器呼叫會升級為使用者端在稽核廣告解析程式階段搜尋的https。

>[!NOTE]
>
>Flash不支援此功能。

使用以下專案來啟用安全廣告載入。 預設不會啟用。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
