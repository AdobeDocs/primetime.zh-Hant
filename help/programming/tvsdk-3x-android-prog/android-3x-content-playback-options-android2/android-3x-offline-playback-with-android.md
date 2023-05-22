---
description: 已引入新的API，這些API將指示TVSDK在下載清單時忽略網路連接狀態。
title: Android離線播放
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Android離線播放 {#offline-playback-with-android}

已引入以下API，它們將指示TVSDK在下載清單時忽略網路連接狀態。 網路連接狀態通常在自適應比特率流(ABR)期間使用，以確定是嘗試回退還是等待網路恢復。

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

您可以啟用此設定並忽略網路連接。

設定 `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` 是真的。 布爾值的預設值為false。

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
