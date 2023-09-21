---
description: TVSDK推出透過HTTPS的安全傳遞。
title: 透過HTTPS的安全傳遞
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 透過HTTPS的安全傳遞 {#secure-delivery-https}

Adobe Primetime TVSDK支援所有來自TVSDK的呼叫的HTTPS傳送，包括

* Auditude廣告伺服器呼叫
* CRS要求
* DRM授權呼叫
* 視訊分析Ping
* 帳單Ping

為了使用此功能，請確保為處理上述請求設定的伺服器支援HTTPS。

預設不會啟用此新行為。 使用以下專案來啟用呼叫前的安全傳遞 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
