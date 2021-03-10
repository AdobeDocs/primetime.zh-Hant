---
title: 透過HTTPS安全載入廣告
description: 透過HTTPS安全載入廣告
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 透過HTTPS {#secure-ad-loading-over-https}安全載入廣告

Adobe Primetime提供選項，可透過HTTPS要求對Primetime廣告伺服器和CRS相關呼叫的首次呼叫。

預設情況下，該功能未啟用。 使用下列功能來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
