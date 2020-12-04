---
description: 您可以使用Adobe Primetime廣告決策介面，將廣告插入VOD和即時／線性內容。
seo-description: 您可以使用Adobe Primetime廣告決策介面，將廣告插入VOD和即時／線性內容。
seo-title: 廣告需求
title: 廣告需求
uuid: 0287f1e4-746f-42e5-b811-409064dd9b13
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 廣告需求{#advertising-requirements}

您可以使用Adobe Primetime廣告決策介面，將廣告插入VOD和即時／線性內容。

<!--<a id="section_A2966DC850E140FE9400A1D9E412F819"></a>-->

Primetime廣告決策可與TVSDK搭配使用，以識別廣告機會、解決廣告，並在視訊串流中插入已解決的廣告。

若要將廣告整合在視訊內容中，請確定廣告和主要視訊內容符合下列需求：

* 廣告內容的HLS版本不能高於主內容的HLS版本。
* 廣告必須多路傳輸，且必須包含僅限音訊的轉譯，不論主要內容是否多路傳輸。
* 廣告播放清單應與主要內容播放清單中的轉譯具有相同的位元速率轉譯。
* 廣告的目標持續時間和個別片段持續時間不能超過主要內容的目標持續時間。
* 如果主要內容包含僅音訊串流，則廣告內容也必須包含僅音訊串流。
* 如果主內容包含字幕流，則廣告內容必須未加密。
* 如果主要內容是多位元速率(MBR)，則廣告內容也必須是MBR。
* 如果主要內容有替代的音軌，則每個廣告必須至少有一個僅限音訊的串流。

如果廣告至少沒有一個僅限音訊的串流，則會略過廣告。