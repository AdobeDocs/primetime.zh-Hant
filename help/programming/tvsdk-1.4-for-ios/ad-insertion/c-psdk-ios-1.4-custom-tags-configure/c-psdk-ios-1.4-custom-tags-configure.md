---
description: 媒體串流可以在播放清單／資訊清單檔案中以標籤形式攜帶其他中繼資料，而此檔案會指出廣告的放置。 您可以指定自訂標籤名稱，並在資訊清單檔案中出現特定標籤時收到通知。
seo-description: 媒體串流可以在播放清單／資訊清單檔案中以標籤形式攜帶其他中繼資料，而此檔案會指出廣告的放置。 您可以指定自訂標籤名稱，並在資訊清單檔案中出現特定標籤時收到通知。
seo-title: 自訂標籤
title: 自訂標籤
uuid: 0f47bed6-2ae8-4e4b-9f6f-672020dc3265
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 概觀 {#custom-tags-overview}

媒體串流可以在播放清單／資訊清單檔案中以標籤形式攜帶其他中繼資料，而此檔案會指出廣告的放置。 您可以指定自訂標籤名稱，並在資訊清單檔案中出現特定標籤時收到通知。

## HLS內容標籤 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>這項功能不適用於Apple電腦上的Safari，因為TVSDK會使用視訊標籤（而非Flash或MSE）來播放HLS內容。

TVSDK針對特定#EXT廣告標籤提供現成可用的支援。 您的應用程式可以使用自訂標籤來增強廣告工作流程或支援封鎖場景。 為支援進階工作流程，TVSDK可讓您指定並訂閱資訊清單中的其他標籤。 當這些標籤出現在資訊清單檔案中時，您會收到通知。

>[!TIP]
>
>您可以訂閱VOD和即時／線性串流的自訂標籤。

>[!NOTE] {othertype=&quot;Limitation&quot;}
>
>當在Safari中使用視訊標籤播放HLS，而非使用Flash備援時，Safari將無法使用此功能。

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

您的應用程式可以設定下列藍本：

* 當標籤或 `#EXT-X-ASSET` 您已訂閱的任何其他自訂標籤名稱集存在於檔案中時，會發出通知。
* 當在串流中找 `#EXT-X-AD` 到標籤或任何其他自訂標籤名稱時插入廣告。

您可以訂閱下列任一標籤作為自訂標籤： `EXT-PROGRAM-DATE-TIME`, `EXT-X-START``EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`。 在剖析資訊清單檔 `TimedMetadata` 案時，會通知您事件。

有些廣告標籤，例 `EXT-X-CUE`如您已訂閱。 這些廣告標籤也由預設機會生成器使用。 通過設定屬性，您可以指定預設業務機會生成器使用哪些廣告 `adTags` 標籤。
