---
title: 安全透過HTTPS載入廣告
description: 安全透過HTTPS載入廣告
copied-description: true
exl-id: f9de1a2b-4eea-4028-83db-1b4021d1fbb7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 安全透過HTTPS載入廣告 {#secure-ad-loading-over-https}

Adobe Primetime提供可透過HTTPS要求第一次呼叫Primetime廣告伺服器和CRS相關呼叫的選項。

預設不會啟用此功能。 使用以下專案來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
