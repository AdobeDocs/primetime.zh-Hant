---
description: 您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。
title: 控制搜尋自訂廣告標籤的播放行為
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# 控制搜尋自訂廣告標籤的播放行為{#control-playback-behavior-for-seeking-over-custom-ad-markers}

您可以覆寫TVSDK在使用自訂廣告標籤時搜尋廣告的預設行為。

依預設，當使用者搜尋自訂廣告標籤放置後所產生的廣告區域或過去廣告區域時，TVSDK會跳過廣告。 這可能與標準廣告插播的目前播放行為不同。

當使用者搜尋超過一或多個自訂廣告時，您可讓TVSDK將播放頭重新定位至最近略過的自訂廣告的開頭。

1. 將`DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED`列舉設定為字串值&quot;true&quot;的中繼資料例項進行設定（不是布林`true`）。

1. 建立並配置`MediaResource`實例，將其他配置選項傳遞到`TimeRangeCollection.toMetadata`。 此方法透過其他一般中繼資料結構接收其他設定選項。

