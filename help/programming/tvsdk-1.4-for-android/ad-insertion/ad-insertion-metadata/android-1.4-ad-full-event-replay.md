---
description: 全事件重播(FER)是一種VOD資產，充當即時/DVR資產，因此您的應用程式必須採取步驟以確保廣告被正確放置。
title: 在全事件重播中啟用廣告
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 在全事件重播中啟用廣告{#enable-ads-in-full-event-replay}

全事件重播(FER)是一種VOD資產，充當即時/DVR資產，因此您的應用程式必須採取步驟以確保廣告被正確放置。

對於即時內容，TVSDK使用清單中的元資料/提示來確定廣告的放置位置。 但是，有時即時/線性內容可能與VOD內容類似。 例如，當即時內容完成時， `EXT-X-ENDLIST` 標籤將附加到即時清單。 對於HLS, `EXT-X-ENDLIST` 標籤表示流是VOD流。 TVSDK無法自動將此流與正常的VOD流區分，以正確插入廣告。

您的應用程式必須通過指定以下內容來告訴TVSDK內容是即時還是視頻點播 `AdSignalingMode`。

對於FER流，Adobe Primetime廣告決定伺服器不應提供在開始播放之前需要在時間線上插入廣告中斷的清單。 這是視頻點播內容的典型過程。 相反，通過指定不同的信令模式，TVSDK從FER清單讀取所有提示點並進入廣告伺服器以請求廣告中斷。 此過程類似於即時/DVR內容。

除了與提示點相關聯的每個請求之外，TVSDK還對預卷廣告進行附加的廣告請求。

1. 從外部源（如vCMS）獲取應使用的信令模式。
1. 建立與廣告相關的元資料。
1. 如果必須覆蓋預設行為，請指定 `AdSignalingMode` 使用 `AdvertisingMetadata.setSignalingMode`。

   有效值為 `DEFAULT, SERVER_MAP`, `MANIFEST_CUES`。

   在調用前必須設定廣告信令模式 `prepareToPlay`。 在TVSDK開始解析廣告並將其置於時間線上後，將忽略對廣告信令模式的更改。 在建立 `AuditudeSettings` 的雙曲餘切值。

1. 繼續播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
