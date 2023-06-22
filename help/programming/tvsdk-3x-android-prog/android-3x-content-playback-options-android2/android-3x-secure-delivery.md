---
description: TVSDK推出透過HTTPS的安全傳送。
title: 透過HTTPS的安全傳遞
exl-id: 41e2c925-2145-4dfd-909a-aec57dbae9cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# 透過HTTPS的安全傳遞 {#secure-delivery-https}

Adobe Primetime TVSDK支援所有來自TVSDK之呼叫的HTTPS傳送，包括

* 稽核廣告伺服器呼叫
* CRS要求
* DRM授權呼叫
* 視訊分析Ping
* 帳單Ping

若要使用此功能，請確定為處理上述請求設定的伺服器支援HTTPS。

預設不會啟用這個新行為。 使用以下專案來啟用呼叫前的安全傳遞 `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
