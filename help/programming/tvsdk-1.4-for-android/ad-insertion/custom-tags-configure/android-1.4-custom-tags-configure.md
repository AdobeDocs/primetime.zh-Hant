---
description: 媒體流可以在播放清單/清單檔案中以標籤形式攜帶附加元資料，並且此檔案指示廣告的放置。 您可以指定自定義標籤名稱，並在清單檔案中出現某些標籤時通知您。
title: 自定義標籤
exl-id: b7528516-4996-4bd3-8a82-bb062973aed5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 概述 {#custom-tags-overview}

媒體流可以在播放清單/清單檔案中以標籤形式攜帶附加元資料，並且此檔案指示廣告的放置。 您可以指定自定義標籤名稱，並在清單檔案中出現某些標籤時通知您。

## HLS內容標籤 {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>此功能在Apple電腦上不可用於Safari，因為TVSDK使用視頻標籤而不是Flash或MSE來播放HLS內容。

TVSDK為特定廣告標籤提供現#EXT支援。 您的應用程式可以使用自定義標籤來增強廣告工作流或支援封鎖方案。 為支援高級工作流，TVSDK允許您指定和訂閱清單中的其他標籤。 當這些標籤出現在清單檔案中時，可以通知您。

>[!TIP]
>
>您可以訂閱VOD和即時/線性流的自定義標籤。

>[!NOTE]
>
>**限制**
>
>使用 `Video` 在Safari中標籤，而不是使用Flash回退，此功能在Safari中將不可用。

## 使用自定義HLS標籤 {#section_AD032318AEF5418393D2B1DF36B0BABB}

下面是自定義VOD資產的示例：

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

您的應用程式可以設定以下方案：

* 在 `#EXT-X-ASSET` 標籤或您訂閱的任何其他自定義標籤名稱集都存在於檔案中。
* 在 `#EXT-X-AD` 在流中找到標籤或任何其他自定義標籤名稱。

可以將下列任何標籤作為自定義標籤訂閱： `EXT-PROGRAM-DATE-TIME`。 `EXT-X-START`。 `EXT-X-AD`。 `EXT-X-CUE`。 `EXT-X-ENDLIST`。 您將收到 `TimedMetadata` 分析清單檔案期間的事件。

有些廣告標籤，例如 `EXT-X-CUE`，您已經訂閱了。 預設機會生成器也使用這些廣告標籤。 通過設定 `adTags` 屬性。
