---
description: TVSDK推出透過HTTPS的安全傳送。
seo-description: TVSDK推出透過HTTPS的安全傳送。
seo-title: 透過HTTPS進行安全傳送
title: 透過HTTPS進行安全傳送
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# 透過HTTPS進行安全傳送 {#secure-delivery-https}

Adobe Primetime TVSDK支援HTTPS傳送來自TVSDK的所有呼叫，其中包括

* Auditude廣告伺服器呼叫
* CRS請求
* DRM授權呼叫
* 視訊分析Ping
* 計費Ping

若要使用此功能，請確定為提供上述請求而設定的伺服器支援HTTPS。

此新行為預設未啟用。 在呼叫前，請使用下列功能來啟用安全傳送 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
