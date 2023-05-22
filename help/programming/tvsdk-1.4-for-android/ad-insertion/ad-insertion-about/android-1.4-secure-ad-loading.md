---
title: 通過HTTPS載入安全廣告
description: 通過HTTPS載入安全廣告
copied-description: true
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# 通過HTTPS載入安全廣告{#secure-ad-loading-over-https}

Adobe Primetime提供了通過HTTPS請求Mighine廣告伺服器和CRS相關呼叫的選項。

預設情況下不啟用該功能。 使用以下命令啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
