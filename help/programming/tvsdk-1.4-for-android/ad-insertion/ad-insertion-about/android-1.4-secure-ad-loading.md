---
title: 安全透過HTTPS載入廣告
description: 安全透過HTTPS載入廣告
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 安全透過HTTPS載入廣告{#secure-ad-loading-over-https}

Adobe Primetime提供可透過HTTPS要求第一次呼叫Primetime廣告伺服器以及CRS相關呼叫的選項。

預設不會啟用此功能。 使用以下專案來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
