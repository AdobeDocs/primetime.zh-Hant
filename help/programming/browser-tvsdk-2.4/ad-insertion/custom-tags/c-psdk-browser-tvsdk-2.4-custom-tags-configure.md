---
description: 媒體串流可以包含其他中繼資料，這些中繼資料會以媒體簡報說明(MPD)檔案中的標籤形式呈現，此檔案會指出廣告的位置。 您可以指定自訂標簽名稱，並在特定標籤出現在資訊清單檔案中時收到通知。
title: 自訂標籤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 概觀 {#custom-tags-overview}

媒體串流可以包含其他中繼資料，這些中繼資料會以媒體簡報說明(MPD)檔案中的標籤形式呈現，此檔案會指出廣告的位置。 您可以指定自訂標簽名稱，並在特定標籤出現在資訊清單檔案中時收到通知。

## HLS內容標籤 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>此功能不適用於Apple電腦上的Safari，因為瀏覽器TVSDK會使用視訊標籤(而非Flash或MSE)來播放HLS內容。

瀏覽器TVSDK為特定#EXT廣告標籤提供立即可用的支援。 您的應用程式可以使用自訂標籤來增強廣告工作流程或支援中斷情況。 為了支援進階工作流程，瀏覽器TVSDK可讓您指定並訂閱資訊清單中的其他標籤。 當這些標籤出現在資訊清單檔案中時，您會收到通知。

>[!TIP]
>
>您可以為VOD和即時/線性串流訂閱自訂標籤。

>[!NOTE]
>
>在Safari中使用「視訊」標籤(而非使用Flash遞補)播放HLS時，此功能將無法在Safari中使用。

## 使用自訂HLS標籤 {#section_AD032318AEF5418393D2B1DF36B0BABB}

以下是自訂VOD資產的範例：

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

您的應用程式可以設定下列案例：

* 發生以下情況時通知： `#EXT-X-ASSET` 標籤或您已訂閱的任何其他自訂標簽名稱集會存在於檔案中。
* 插入廣告的時機 `#EXT-X-AD` 標籤或任何其他自訂標簽名稱，可在資料流中找到。

您可以訂閱下列任何標籤作為自訂標籤： `EXT-PROGRAM-DATE-TIME`， `EXT-X-START`， `EXT-X-AD`， `EXT-X-CUE`， `EXT-X-ENDLIST`. 系統會通知您 `TimedMetadata` 分析資訊清單檔案期間發生的事件。

有一些廣告標籤，例如 `EXT-X-CUE`，您已訂閱此資訊。 這些廣告標籤也會由預設機會產生器使用。 您可以透過設定 `adTags` 屬性。

## 虛線內容標籤 {#section_967A952319BE4048B4C6612FFF7ADA6E}

DASH有兩種傳送事件訊號的方式：

* 在MPD檔案中。

  此檔案類似於HLS內容中的M3U8檔案，且.mpd檔案中存在MPD事件。
* 表示中的內嵌

  藉由將事件訊息新增為區段的一部分，帶內事件與表示相互複用。 代表是依序播放的視訊與音訊區段清單。 內嵌事件資料會嵌入到這些區段中。

這些事件會通知為 `TimedMetadata` 一經瀏覽器TVSDK剖析事件，立即傳送給應用程式。 一旦事件收到通知，就不會再次收到通知。
