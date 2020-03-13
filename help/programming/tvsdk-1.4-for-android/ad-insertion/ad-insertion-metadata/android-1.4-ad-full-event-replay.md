---
description: 完整事件重播(FER)是VOD資產，可當成即時/DVR資產，因此您的應用程式必須採取步驟，以確保正確放置廣告。
seo-description: 完整事件重播(FER)是VOD資產，可當成即時/DVR資產，因此您的應用程式必須採取步驟，以確保正確放置廣告。
seo-title: 在完整事件重播中啟用廣告
title: 在完整事件重播中啟用廣告
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在完整事件重播中啟用廣告{#enable-ads-in-full-event-replay}

完整事件重播(FER)是VOD資產，可當成即時/DVR資產，因此您的應用程式必須採取步驟，以確保正確放置廣告。

對於即時內容，TVSDK會使用資訊清單中的中繼資料／提示來決定放置廣告的位置。 不過，有時即時／線性內容可能與VOD內容相似。 例如，當即時內容完成時，即 `EXT-X-ENDLIST` 時資訊清單會附加標籤。 對於HLS，標 `EXT-X-ENDLIST` 記表示該串流是VOD串流。 TVSDK無法自動區分此串流與一般VOD串流，以正確插入廣告。

您的應用程式必須透過指定來告知TVSDK內容是即時或VOD `AdSignalingMode`。

對於FER串流，Adobe Primetime廣告決策伺服器不應提供在開始播放之前必須先插入時間軸的廣告插播清單。 這是VOD內容的典型程式。 相反地，TVSDK透過指定不同的信令模式，從FER資訊清單讀取所有提示點，並前往廣告伺服器，以請求廣告中斷。 此程式類似於即時/DVR內容。

除了與提示點相關的每個要求外，TVSDK還會針對前段廣告提出額外的廣告要求。

1. 從外部源（如vCMS）獲取應使用的信令模式。
1. 建立廣告相關的中繼資料。
1. 如果必須覆寫預設行為，請使 `AdSignalingMode` 用指定 `AdvertisingMetadata.setSignalingMode`。

   有效值是 `DEFAULT, SERVER_MAP`和 `MANIFEST_CUES`。

   您必須先設定廣告信令模式，再進行呼叫 `prepareToPlay`。 在TVSDK開始解析廣告並將其置於時間軸上後，會忽略對廣告訊號模式的變更。 在建立對象時設定模 `AuditudeSettings` 式。

1. 繼續播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

