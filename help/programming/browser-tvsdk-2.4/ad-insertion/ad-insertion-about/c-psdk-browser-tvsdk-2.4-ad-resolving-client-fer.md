---
description: 完整事件重播(FER)內容是即時串流，透過將#EXT-X-ENDLIST標籤新增至資訊清單檔案的結尾，轉換為VOD。 該串流保留其廣告提示標籤。
seo-description: 完整事件重播(FER)內容是即時串流，透過將#EXT-X-ENDLIST標籤新增至資訊清單檔案的結尾，轉換為VOD。 該串流保留其廣告提示標籤。
seo-title: FER廣告解析和插入
title: FER廣告解析和插入
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# FER廣告解析和插入{#fer-ad-resolving-and-insertion}

完整事件重播(FER)內容是即時串流，透過將#EXT-X-ENDLIST標籤新增至資訊清單檔案的結尾，轉換為VOD。 該串流保留其廣告提示標籤。

瀏覽器TVSDK將FER串流視為VOD，因此預設廣告信令模式為 `SERVER_MAP`。 不過，由於串流會保留其廣告提示標籤，因此您可以將廣告信令模式設定為 `MANIFEST_CUES`，讓您使用廣告插入的廣告提示標籤。

若要針對FER串流使用提示標籤來開啟廣告插入：

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER廣告解析和插入行為與即時廣告解析和插入類似。 瀏覽器TVSDK會執行下列動作：

1. 在內容開頭插入任何前置廣告。
1. 解析資訊清單中定義的提示點所指定的廣告。
1. 以相同持續時間的廣告分段取代主要內容的部分
1. 視需要重新計算虛擬時間軸。

**限制：** 瀏覽器TVSDK僅支援HLS FER串流播放。 此外，FER串流不支援MP4中端廣告。
