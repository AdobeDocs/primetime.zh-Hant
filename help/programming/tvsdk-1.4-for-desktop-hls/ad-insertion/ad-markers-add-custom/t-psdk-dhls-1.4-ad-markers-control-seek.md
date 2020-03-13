---
description: 您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。
seo-description: 您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。
seo-title: 控制搜尋自訂廣告標籤的播放行為
title: 控制搜尋自訂廣告標籤的播放行為
uuid: 926299c6-9c23-457d-b836-08432e4e169e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 控制搜尋自訂廣告標籤的播放行為{#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。

依預設，當使用者搜尋自訂廣告標籤放置後所產生的廣告區域或過去廣告區域時，TVSDK會跳過廣告。 這可能與標準廣告插播的目前播放行為不同。

當使用者搜尋超過一或多個自訂廣告時，您可讓TVSDK將播放頭重新定位至最近略過的自訂廣告的開頭。

1. 設定中繼資料例項， `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` 枚舉設為字串值&quot;true&quot;(非布林 `true`值)。

1. 建立並設定 `MediaResource` 例項，將其他設定選項傳遞至 `TimeRangeCollection.toMetadata`。 此方法透過其他一般中繼資料結構接收其他設定選項。

