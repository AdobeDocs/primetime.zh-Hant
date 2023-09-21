---
description: 您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。
title: 控制對自訂廣告標籤進行搜尋的播放行為
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 控制對自訂廣告標籤進行搜尋的播放行為{#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。

根據預設，當使用者搜尋或越過自訂廣告標籤放置造成的廣告區段時，TVSDK會略過廣告。 這可能與標準廣告插播目前的播放行為不同。

您可以指示TVSDK在使用者搜尋超過一或多個自訂廣告時，將播放點重新定位至最近略過的自訂廣告開頭。

1. 使用設定中繼資料例項 `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 列舉已設定為字串值「true」（不是布林值） `true`)。

1. 建立及設定 `MediaResource` 執行個體，將其他設定選項傳遞至 `TimeRangeCollection.toMetadata`. 此方法會透過其他一般中繼資料結構接收其他設定選項。
