---
description: 當瀏覽器TVSDK要求不在您主要廣告伺服器上的廣告時，播放器需要向次要伺服器要求廣告。 視訊廣告服務範本(VAST)設定廣告伺服器與視訊播放器之間通訊的標準，是次要廣告伺服器在要求廣告時所傳送的回應。
title: 廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# 廣泛廣告{#vast-ads}

當瀏覽器TVSDK要求不在您主要廣告伺服器上的廣告時，播放器需要向次要伺服器要求廣告。 視訊廣告服務範本(VAST)設定廣告伺服器與視訊播放器之間通訊的標準，是次要廣告伺服器在要求廣告時所傳送的回應。

如需VAST的詳細資訊，請參閱[數位視訊廣告服務範本(VAST)3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)。

瀏覽器TVSDK支援下列VAST廣告元素：

## 包裝函式與內嵌廣告{#section_11B8A1A8F52F4F77981C6AAC02185087}

支援下列元素：

* **`wrapper`** 當播放器需要連絡次要廣告伺服器以請求廣告時，包裝函式元素會提供重新導向資訊。一個包裝函式元素可以指向數個包裝函式，最終指向VAST廣告。

* **`inline`** 支援下列必要元素：

* `AdSystem`
* `AdTitle`
* `Impression`

   支援下列選用元素：

* `Description`
* `Survey`
* `Error`

## 創意{#section_0121F948CB074E49A8132D202786CAA4}

此元素是VAST廣告的一部分，並包含`creative`元素，可支援線性廣告、非線性廣告或配套廣告。 在`creative`元素中，`id`、`sequence`和`adId`元素受支援。

以下是廣告類型的詳細資訊：

* **線性** 廣告支援下列元素：

   * `TrackingEvent`，其中包含 `Tracking` 元素。
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
         >在此元素中，`id`、`bitrate`、`delivery`、`width`、`height`、`scalable`、`maintainAspectRatio`、`apiFramework`和`type`屬性受支援。

* **非線性廣** 告支援下列元素：

   * `Non-linear`

      >[!TIP]
      >
      >在此元素中，`id`、`width`、`height`、`apiFramework`、`expandedWidth`、`expandedHeight`、`scalable`、`maintainAspectRatio`和`minSuggestedDuration`屬性受支援。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **配套** 廣告支援下列元素：

   * `Companion`

      >[!TIP]
      >
      >在此元素中，`id`、`width`、`height`、`apiFramework`、`expandedWidth`和`expandedHeight`屬性受支援。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 副檔名{#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>僅支援Auditude專用的擴充功能。

* `Extension`
