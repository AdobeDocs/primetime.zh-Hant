---
description: MediaPlayerItem.timedMetadata屬性可讓您存取所有從播放清單／資訊清單標籤或從媒體串流中的ID3標籤建立的TimedMetadata物件。
title: 資訊清單標籤的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性可讓您存取所有從播放清單／資訊清單標籤或從媒體串流中的ID3標籤建立的TimedMetadata物件。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

`MediaPlayerItem.hasTimedMetadata`屬性指示當前介質中是否存在預訂的自定義標籤。 您可以監聽`Events.TimedMetadataEvent`的計時中繼資料，MediaPlayer例項會在每次建立新`TimedMetadata`物件時進行分派。
