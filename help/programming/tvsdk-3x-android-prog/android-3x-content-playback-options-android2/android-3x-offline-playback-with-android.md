---
description: 已引入新API，指示TVSDK在下載資訊清單時忽略網路連線狀態。
title: 使用Android離線播放
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 使用Android離線播放 {#offline-playback-with-android}

已引入下列API，指示TVSDK在下載資訊清單時忽略網路連線狀態。 網路連線狀態通常用於最適化位元速率串流(ABR)期間，以判斷是否要嘗試遞補或等待網路恢復。

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

您可以啟用此設定並忽略網路連線。

設定 `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` 為true。 布林值的預設值為false。

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
