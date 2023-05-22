---
description: 當瀏覽器TVSDK請求主廣告伺服器上沒有的廣告時，播放器需要從輔助伺服器請求廣告。 視頻廣告服務模板(VAST)設定廣告伺服器和視頻播放器之間通信的標準，是在請求廣告時由輔助廣告伺服器發送的響應。
title: 廣告
exl-id: b0ebade5-b5da-413d-84f4-abebac579f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 廣告 {#vast-ads}

當瀏覽器TVSDK請求主廣告伺服器上沒有的廣告時，播放器需要從輔助伺服器請求廣告。 視頻廣告服務模板(VAST)設定廣告伺服器和視頻播放器之間通信的標準，是在請求廣告時由輔助廣告伺服器發送的響應。

有關VAST的詳細資訊，請參見 [數字視頻廣告服務模板(VAST)3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)。

瀏覽器TVSDK支援以下VAST廣告元素：

## 包裝和內聯廣告 {#section_11B8A1A8F52F4F77981C6AAC02185087}

支援以下元素：

* **`wrapper`** 當播放器需要聯繫輔助廣告伺服器以請求廣告時，包裝器元素提供重定向資訊。 一個包裝元素可以指向幾個包裝，最終指向一個VAST廣告。

* **`inline`** 支援以下必需元素：

* `AdSystem`
* `AdTitle`
* `Impression`

   支援以下可選元素：

* `Description`
* `Survey`
* `Error`

## 創意 {#section_0121F948CB074E49A8132D202786CAA4}

此元素是VAST廣告的一部分，並包含 `creative` 支援線性廣告、非線性廣告或伴生廣告的元素。 在 `creative` 元素 `id`。 `sequence`, `adId` 支援元素。

以下是有關廣告類型的詳細資訊：

* **線性廣告** 支援以下元素：

   * `TrackingEvent`，其中包含 `Tracking` 的子菜單。
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
         >在此元素中， `id`。 `bitrate`。 `delivery`。 `width`。 `height`。 `scalable`。 `maintainAspectRatio`。 `apiFramework`, `type` 支援屬性。

* **非線性廣告** 支援以下元素：

   * `Non-linear`

      >[!TIP]
      >
      >在此元素中， `id`。 `width`。 `height`。 `apiFramework`。 `expandedWidth`。 `expandedHeight`。 `scalable`。 `maintainAspectRatio`, `minSuggestedDuration` 支援屬性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **伴侶廣告** 支援以下元素：

   * `Companion`

      >[!TIP]
      >
      >在此元素中， `id`。 `width`。 `height`。 `apiFramework`。 `expandedWidth`, `expandedHeight` 支援屬性。

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## 擴展 {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>僅支援特定於Auditude的擴展。

* `Extension`
