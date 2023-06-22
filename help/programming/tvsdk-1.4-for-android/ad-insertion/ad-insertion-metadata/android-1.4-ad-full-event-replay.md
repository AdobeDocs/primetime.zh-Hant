---
description: 完整事件重播(FER)是一種可作為即時/DVR資產的VOD資產，因此您的應用程式必須採取措施以確保廣告正確放置。
title: 啟用完整事件重播中的廣告
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 啟用完整事件重播中的廣告{#enable-ads-in-full-event-replay}

完整事件重播(FER)是一種可作為即時/DVR資產的VOD資產，因此您的應用程式必須採取措施以確保廣告正確放置。

對於即時內容，TVSDK會使用資訊清單中的中繼資料/提示來決定放置廣告的位置。 不過，有時即時/線性內容可能會類似VOD內容。 例如，當即時內容完成時， `EXT-X-ENDLIST` 標籤會附加至即時資訊清單。 若為HLS，則 `EXT-X-ENDLIST` 標籤表示資料流是VOD資料流。 TVSDK無法自動區分此串流和一般VOD串流，以正確插入廣告。

您的應用程式必須透過指定 `AdSignalingMode`.

對於FER資料流，Adobe Primetime ad decisioning伺服器不應提供在開始播放之前需要插入時間軸上的廣告插播清單。 這是VOD內容的典型程式。 相反地，透過指定不同的訊號模式，TVSDK會從FER資訊清單中讀取所有提示點，並前往每個提示點的廣告伺服器，以請求廣告插播。 此程式類似於即時/DVR內容。

除了與提示點關聯的每個請求之外，TVSDK還會針對前段廣告提出額外的廣告請求。

1. 從外部來源（例如vCMS）取得應使用的訊號模式。
1. 建立廣告相關中繼資料。
1. 如果必須覆寫預設行為，請指定 `AdSignalingMode` 透過使用 `AdvertisingMetadata.setSignalingMode`.

   有效值為 `DEFAULT, SERVER_MAP`、和 `MANIFEST_CUES`.

   呼叫之前，您必須設定廣告訊號模式 `prepareToPlay`. 在TVSDK開始解析廣告並將廣告置於時間軸上後，廣告訊號模式的變更會被忽略。 建立時設定模式 `AuditudeSettings` 物件。

1. 繼續播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
