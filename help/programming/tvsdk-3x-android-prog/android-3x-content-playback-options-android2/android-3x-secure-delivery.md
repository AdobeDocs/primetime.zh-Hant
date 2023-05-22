---
description: TVSDK引入了通過HTTPS的安全傳送。
title: 通過HTTPS安全傳遞
exl-id: 41e2c925-2145-4dfd-909a-aec57dbae9cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 通過HTTPS安全傳遞 {#secure-delivery-https}

Adobe PrimetimeTVSDK為來自TVSDK的所有呼叫提供HTTPS傳送支援，包括

* 審核廣告伺服器呼叫
* CRS請求
* DRM許可呼叫
* 視頻分析Ping
* 計費ping

為了使用此功能，請確保為提供上述請求服務而配置的伺服器支援HTTPS。

預設情況下不啟用此新行為。 使用以下選項在呼叫前啟用安全傳遞 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
