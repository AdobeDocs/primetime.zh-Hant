---
description: 完整事件重播(FER)內容是指將#EXT-X-ENDLIST標籤新增至資訊清單檔案的結尾處，藉此轉換為VOD的即時資料流。 串流會保留其廣告提示標籤。
title: FER廣告解析和插入
exl-id: 9075932d-4e77-4249-af5d-0b392033907f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# FER廣告解析和插入{#fer-ad-resolving-and-insertion}

完整事件重播(FER)內容是指將#EXT-X-ENDLIST標籤新增至資訊清單檔案的結尾處，藉此轉換為VOD的即時資料流。 串流會保留其廣告提示標籤。

瀏覽器TVSDK會將FER資料流視為VOD，所以預設的廣告訊號模式為 `SERVER_MAP`. 不過，由於串流會保留其廣告提示標籤，因此您可以將廣告訊號模式設定為 `MANIFEST_CUES`，可讓您使用廣告提示標籤來插入廣告。

若要使用FER資料流的提示標籤來開啟廣告插入：

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER廣告解析和插入行為類似於即時廣告解析和插入。 瀏覽器TVSDK會執行下列動作：

1. 在內容的開頭插入任何前段廣告。
1. 解析資訊清單中定義的提示點所指定的廣告。
1. 以相同持續時間的廣告插播取代部分主要內容
1. 如有必要，請重新計算虛擬時間表。

**限制：** 瀏覽器TVSDK僅支援HLS FER資料流播放。 此外，FER資料流不支援MP4中段廣告。
