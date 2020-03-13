---
description: 'null'
seo-description: 'null'
seo-title: 透過HTTPS安全載入廣告
title: 透過HTTPS安全載入廣告
uuid: 0d680fef-a372-4157-a89b-d9f10003c768
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 透過HTTPS安全載入廣告{#secure-ad-loading-over-https}

Adobe Primetime提供選項，可透過HTTPS要求對Primetime廣告伺服器和CRS相關呼叫的首次呼叫。

預設情況下，該功能未啟用。 使用下列功能來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

