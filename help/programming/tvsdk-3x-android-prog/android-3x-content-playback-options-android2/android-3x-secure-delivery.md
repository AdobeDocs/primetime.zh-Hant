---
description: TVSDK推出透過HTTPS的安全傳送。
title: 透過HTTPS進行安全傳送
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# 透過HTTPS {#secure-delivery-https}的安全傳送

Adobe PrimetimeTVSDK支援HTTPS傳送所有源自TVSDK的呼叫，其中包括

* Auditude廣告伺服器呼叫
* CRS請求
* DRM授權呼叫
* 視訊分析Ping
* 計費Ping

若要使用此功能，請確定為提供上述請求而設定的伺服器支援HTTPS。

此新行為預設未啟用。 在呼叫`MediaPlayer.replaceCurrentResource()`之前，請使用下列功能啟用安全傳送

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
