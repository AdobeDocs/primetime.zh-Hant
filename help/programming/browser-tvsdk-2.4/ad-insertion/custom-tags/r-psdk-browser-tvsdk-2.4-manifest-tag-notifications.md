---
description: MediaPlayerItem.timedMetadata屬性提供存取所有TimedMetadata物件的功能，這些物件是從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的。
title: 資訊清單標籤的通知
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 資訊清單標籤的通知{#notifications-for-manifest-tags}

MediaPlayerItem.timedMetadata屬性提供存取所有TimedMetadata物件的功能，這些物件是從播放清單/資訊清單標籤或媒體串流中的ID3標籤建立的。

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

此 `MediaPlayerItem.hasTimedMetadata` 屬性指出目前媒體中是否存在訂閱的自訂標籤。 您可以透過聆聽 `Events.TimedMetadataEvent`，MediaPlayer例項會在每次新增時傳送此訊息 `TimedMetadata` 物件已建立。
