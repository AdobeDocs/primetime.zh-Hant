---
description: MediaPlayerItem.timedMetadata屬性可讓您存取所有從播放清單／資訊清單標籤或從媒體串流中的ID3標籤建立的TimedMetadata物件。
seo-description: MediaPlayerItem.timedMetadata屬性可讓您存取所有從播放清單／資訊清單標籤或從媒體串流中的ID3標籤建立的TimedMetadata物件。
seo-title: 資訊清單標籤的通知
title: 資訊清單標籤的通知
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性可讓您存取所有從播放清單／資訊清單標籤或從媒體串流中的ID3標籤建立的TimedMetadata物件。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

屬性 `MediaPlayerItem.hasTimedMetadata` 會指出目前媒體中是否存在已訂閱的自訂標籤。 您可以監聽計時中繼資料， `Events.TimedMetadataEvent`MediaPlayer例項會在每次建立新物件時調 `TimedMetadata` 度該中繼資料。
