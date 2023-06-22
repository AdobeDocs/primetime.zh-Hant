---
description: 當瀏覽器TVSDK請求不在主要廣告伺服器上的廣告時，播放器需要從次要伺服器請求廣告。 視訊廣告服務範本(VAST)會設定廣告伺服器和視訊播放器之間的通訊標準，以及次要廣告伺服器在請求廣告時傳送的回應。
title: VAST廣告
exl-id: b0ebade5-b5da-413d-84f4-abebac579f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# VAST廣告 {#vast-ads}

當瀏覽器TVSDK請求不在主要廣告伺服器上的廣告時，播放器需要從次要伺服器請求廣告。 視訊廣告服務範本(VAST)會設定廣告伺服器和視訊播放器之間的通訊標準，以及次要廣告伺服器在請求廣告時傳送的回應。

如需VAST的詳細資訊，請參閱 [數位視訊廣告服務範本(VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

瀏覽器TVSDK支援下列VAST廣告元素：

## 包裝函式和內嵌廣告 {#section_11B8A1A8F52F4F77981C6AAC02185087}

支援下列元素：

* **`wrapper`** 當播放器需要聯絡次要廣告伺服器以請求廣告時，包裝函式元素會提供重新導向資訊。 一個包裝函式元素可以指向數個最終指向VAST廣告的包裝函式。

* **`inline`** 支援下列必要元素：

* `AdSystem`
* `AdTitle`
* `Impression`

   支援下列選用元素：

* `Description`
* `Survey`
* `Error`

## 創意 {#section_0121F948CB074E49A8132D202786CAA4}

此元素是屬於VAST廣告一部分的檔案，並包含 `creative` 可支援線性廣告、非線性廣告或隨附廣告的元素。 在 `creative` 元素， `id`， `sequence`、和 `adId` 支援元素。

以下是有關廣告型別的詳細資訊：

* **線性廣告** 支援下列元素：

   * `TrackingEvent`，其中包含 `Tracking` 元素。
      * `Duration`
      * `AdParameters`
      * `VideoClicks`，包括下列專案：

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >在此元素中， `id`， `bitrate`， `delivery`， `width`， `height`， `scalable`， `maintainAspectRatio`， `apiFramework`、和 `type` 屬性受到支援。

* **非線性廣告** 支援下列元素：

   * `Non-linear`

      >[!TIP]
      >
      >在此元素中， `id`， `width`， `height`， `apiFramework`， `expandedWidth`， `expandedHeight`， `scalable`， `maintainAspectRatio`、和 `minSuggestedDuration` 屬性受到支援。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **隨附廣告** 支援下列元素：

   * `Companion`

      >[!TIP]
      >
      >在此元素中， `id`， `width`， `height`， `apiFramework`， `expandedWidth`、和 `expandedHeight` 屬性受到支援。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 擴充功能 {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>僅支援Auditude特定的擴充功能。

* `Extension`
