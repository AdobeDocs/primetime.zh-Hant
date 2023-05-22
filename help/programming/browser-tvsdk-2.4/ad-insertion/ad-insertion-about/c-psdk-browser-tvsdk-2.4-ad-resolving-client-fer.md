---
description: 全事件重播(FER)內容是通過將#EXT-X-ENDLIST標籤添加到清單檔案末尾而轉換為VOD的即時流。 流保留其廣告提示標籤。
title: FER廣告解析和插入
exl-id: 9075932d-4e77-4249-af5d-0b392033907f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# FER廣告解析和插入{#fer-ad-resolving-and-insertion}

全事件重播(FER)內容是通過將#EXT-X-ENDLIST標籤添加到清單檔案末尾而轉換為VOD的即時流。 流保留其廣告提示標籤。

瀏覽器TVSDK將FER流視為VOD，因此預設情況下，廣告信令模式是 `SERVER_MAP`。 但是，由於流保留其ad提示標籤，因此可以將ad信令模式設定為 `MANIFEST_CUES`，用於使用ad提示標籤進行ad插入。

要使用FER流的提示標籤開啟和插入：

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

FER和解析和插入行為類似於即時和解析和插入。 瀏覽器TVSDK執行以下操作：

1. 在內容開頭插入任何預卷廣告。
1. 解析由清單中定義的提示點指定的廣告。
1. 用相同持續時間的廣告分段替換主內容的部分
1. 如有必要，重新計算虛擬時間線。

**限制：** 瀏覽器TVSDK僅支援HLS FER流回放。 此外，FER流不支援MP4中間卷廣告。
