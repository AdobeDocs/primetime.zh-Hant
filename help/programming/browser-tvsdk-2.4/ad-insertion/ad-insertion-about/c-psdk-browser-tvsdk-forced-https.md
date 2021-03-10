---
title: 透過HTTPS安全載入廣告
description: 透過HTTPS安全載入廣告
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 透過HTTPS安全載入廣告{#secure-ad-loading-over-https}

Adobe Primetime可以透過https要求協力廠商廣告伺服器，即使播放器是以http代管。 只有這些廣告伺服器呼叫會升級至用戶端在Auditude Ad解析程式階段期間所搜尋的https。

>[!NOTE]
>
>這項功能不支援Flash。

使用下列功能來啟用安全廣告載入。 預設未啟用。

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
