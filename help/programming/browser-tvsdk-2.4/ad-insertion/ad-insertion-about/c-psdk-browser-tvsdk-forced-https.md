---
title: 安全透過HTTPS載入廣告
description: 安全透過HTTPS載入廣告
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# 安全透過HTTPS載入廣告{#secure-ad-loading-over-https}

即使播放器託管於http上，Adobe Primetime仍可透過https要求協力廠商廣告伺服器。 只有這些廣告伺服器呼叫會升級為使用者端在Auditude廣告解析程式階段搜尋的https。

>[!NOTE]
>
>Flash不支援此功能。

使用以下專案來啟用安全廣告載入。 預設不會啟用。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
