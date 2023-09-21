---
description: 已引入新的API，將指示TVSDK在下載資訊清單時忽略網路連線狀態。
title: 使用Android離線播放
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 使用Android離線播放 {#offline-playback-with-android}

已引入下列API，將指示TVSDK在下載資訊清單時忽略網路連線狀態。 網路連線狀態通常用於最適化位元速率串流(ABR)期間，以判斷要嘗試遞補或等待網路恢復。

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
