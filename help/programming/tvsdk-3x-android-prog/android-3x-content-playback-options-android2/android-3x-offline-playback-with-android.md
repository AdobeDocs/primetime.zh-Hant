---
description: '已引入新的API，可指示TVSDK在下載清單時忽略網路連線狀態。 '
seo-description: '已引入新的API，可指示TVSDK在下載清單時忽略網路連線狀態。 '
seo-title: 使用Android的離線播放
title: 使用Android的離線播放
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 使用Android的離線播放 {#offline-playback-with-android}

已引入下列API，可指示TVSDK在下載清單時忽略網路連線狀態。 網路連接狀態通常用於自適應位元速率流(ABR)，以確定是嘗試備援還是等待網路恢復。

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

您可以啟用此設定並忽略網路連接。

設 `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` 為true。 布林值的預設值為false。

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
