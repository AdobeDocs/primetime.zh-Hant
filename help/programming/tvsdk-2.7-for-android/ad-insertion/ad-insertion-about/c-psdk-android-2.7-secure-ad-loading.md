---
description: 'null'
seo-description: 'null'
seo-title: 透過HTTPS安全載入廣告
title: 透過HTTPS安全載入廣告
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 透過HTTPS安全載入廣告 {#secure-ad-loading-over-https}

Adobe Primetime提供選項，可透過HTTPS要求對Primetime廣告伺服器和CRS相關呼叫的首次呼叫。

預設情況下，該功能未啟用。 使用下列功能來啟用安全廣告載入。

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

