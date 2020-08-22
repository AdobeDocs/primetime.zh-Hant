---
description: 當瀏覽器TVSDK要求不在您主要廣告伺服器上的廣告時，播放器需要向次要伺服器要求廣告。 視訊廣告服務範本(VAST)設定廣告伺服器與視訊播放器之間通訊的標準，是次要廣告伺服器在要求廣告時所傳送的回應。
seo-description: 當瀏覽器TVSDK要求不在您主要廣告伺服器上的廣告時，播放器需要向次要伺服器要求廣告。 視訊廣告服務範本(VAST)設定廣告伺服器與視訊播放器之間通訊的標準，是次要廣告伺服器在要求廣告時所傳送的回應。
seo-title: 廣告
title: 廣告
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 廣告 {#vast-ads}

當瀏覽器TVSDK要求不在您主要廣告伺服器上的廣告時，播放器需要向次要伺服器要求廣告。 視訊廣告服務範本(VAST)設定廣告伺服器與視訊播放器之間通訊的標準，是次要廣告伺服器在要求廣告時所傳送的回應。

如需有關VAST的詳細資訊，請 [參閱數位視訊廣告服務範本(VAST)3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)。

瀏覽器TVSDK支援下列VAST廣告元素：

## 包裝函式與內嵌廣告 {#section_11B8A1A8F52F4F77981C6AAC02185087}

支援下列元素：

* **`wrapper`** 當播放器需要連絡次要廣告伺服器以請求廣告時，包裝函式元素會提供重新導向資訊。 一個包裝函式元素可以指向數個包裝函式，最終指向VAST廣告。

* **`inline`** 支援下列必要元素：

* `AdSystem`
* `AdTitle`
* `Impression`

   支援下列選用元素：

* `Description`
* `Survey`
* `Error`

## 創意人員 {#section_0121F948CB074E49A8132D202786CAA4}

此元素是VAST廣告的一部分，並包含可支 `creative` 援線性廣告、非線性廣告或配套廣告的元素。 在元 `creative` 素中， `id`支援 `sequence`、和 `adId` 元素。

以下是廣告類型的詳細資訊：

* **線性廣告** ：支援下列元素：

   * `TrackingEvent`，其中包含元 `Tracking` 素。
      * `Duration`
      * `AdParameters`
      * `VideoClicks`，包括：

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >在此元素中，支 `id`持、 `bitrate`、、 `delivery`、 `width`、、 `height`和屬 `scalable``maintainAspectRatio``apiFramework``type` 性。

* **非線性廣告** ：支援下列元素：

   * `Non-linear`

      >[!TIP]
      >
      >在此元素中，支 `id`持、 `width`、、 `height`、 `apiFramework`、、 `expandedWidth`和屬 `expandedHeight``scalable``maintainAspectRatio``minSuggestedDuration` 性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **配套廣告** ：支援下列元素：

   * `Companion`

      >[!TIP]
      >
      >在此元素中，支 `id`持、 `width`、 `height`、 `apiFramework``expandedWidth`和 `expandedHeight` 屬性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 擴充功能 {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>僅支援Auditude專用的擴充功能。

* `Extension`
