---
description: 完整事件重播(FER)是一種可作為即時/DVR資產的VOD資產，因此您的應用程式必須採取措施以確保廣告正確放置。
title: 在全事件重播中啟用廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 在全事件重播中啟用廣告{#enable-ads-in-full-event-replay}

完整事件重播(FER)是一種可作為即時/DVR資產的VOD資產，因此您的應用程式必須採取措施以確保廣告正確放置。

對於即時內容，TVSDK會使用資訊清單中的中繼資料/提示來決定放置廣告的位置。 不過，有時即時/線性內容可能會類似VOD內容。 例如，當即時內容完成時， `EXT-X-ENDLIST` 標籤會附加至即時資訊清單。 若為HLS，則為 `EXT-X-ENDLIST` 標籤表示資料流是VOD資料流。 TVSDK無法自動將此資料流與一般VOD資料流區分開來，以便正確插入廣告。

您的應用程式必須透過指定 `AdSignalingMode`.

對於FER資料流，Adobe Primetime ad decisioning伺服器不應提供在開始播放之前需要在時間軸上插入的廣告插播清單。 這是VOD內容的典型程式。 相反地，透過指定不同的訊號模式，TVSDK會從FER資訊清單讀取所有提示點，並前往廣告伺服器讓每個提示點請求廣告插播。 此程式類似於即時/DVR內容。

除了與提示點相關聯的每個請求之外，TVSDK還會針對前段廣告提出額外的廣告請求。

1. 從外部來源（例如vCMS）取得應使用的訊號模式。
1. 建立廣告相關中繼資料。
1. 如果預設行為必須覆寫，請指定 `AdSignalingMode` 藉由使用 `AdvertisingMetadata.setSignalingMode`.

   有效值為 `DEFAULT, SERVER_MAP`、和 `MANIFEST_CUES`.

   呼叫之前，您必須設定廣告訊號模式 `prepareToPlay`. 在TVSDK開始解析廣告並將其放置在時間軸上後，廣告訊號模式的變更會被忽略。 建立時設定模式 `AuditudeSettings` 物件。

1. 繼續播放。

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
