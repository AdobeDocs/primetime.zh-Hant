---
description: 'null'
seo-description: 'null'
seo-title: 透過HTTPS安全載入廣告
title: 透過HTTPS安全載入廣告
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---


# 透過HTTPS安全載入廣告{#secure-ad-loading-over-https}

Adobe Primetime可透過https要求第三方廣告伺服器，即使播放器是以http代管亦然。 只有這些廣告伺服器呼叫會升級至用戶端在Auditude Ad解析程式階段期間所搜尋的https。

>[!NOTE]
>
>Flash不支援此功能。

使用下列功能來啟用安全廣告載入。 預設未啟用。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
