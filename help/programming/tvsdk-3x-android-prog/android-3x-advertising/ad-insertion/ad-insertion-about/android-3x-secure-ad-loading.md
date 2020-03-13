---
description: 'null'
seo-description: 'null'
seo-title: 透過HTTPS安全載入廣告
title: 透過HTTPS安全載入廣告
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 透過HTTPS安全載入廣告 {#secure-ad-loading-over-https}

Adobe Primetime提供選項，可透過HTTPS要求對Primetime廣告伺服器和CRS相關呼叫的首次呼叫。

預設情況下，該功能未啟用。 使用下列功能來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
