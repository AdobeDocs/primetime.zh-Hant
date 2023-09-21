---
description: 您可以搭配StageVideo使用HTML覆蓋圖，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo會始終顯示在任何Flash顯示清單元素後面。
title: StageVideo和HTML覆蓋圖
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo和HTML覆蓋圖{#stagevideo-and-html-overlays}

您可以搭配StageVideo使用HTML覆蓋圖，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo會始終顯示在任何Flash顯示清單元素後面。

HTML覆蓋圖是UI元素，您可在轉譯之視訊的Flash顯示平面中顯示 `StageVideo` 在它自己的平面上。 在Flash15之前，如果無法取得硬體加速，就無法使用HTML覆蓋。 從Flash15開始，HTML覆蓋圖會在 `StageVideo` 退回至軟體轉譯。

>[!IMPORTANT]
>
>當您使用HTML覆蓋圖時，效能可能會或多或少地降低，具體取決於您的系統功能。

考量下列資訊：

* 在Flash Player15中：

   * 無論硬體加速是否可用，您都可以使用HTML覆蓋。
   * 若要使用HTML覆蓋圖，請設定 `wmode` 至 `opaque`.

* 在Flash Player14中：

   * 硬體加速可用時， `StageVideo` 位在Flash顯示清單下方，因此您可以使用HTML覆蓋圖。
   * 無法使用硬體加速時，視訊會呈現於瀏覽器中所有其他元素上方，以避免使用HTML覆蓋圖。

以下為搭配使用HTML覆蓋圖的最低瀏覽器需求 `StageVideo`：

* Firefox版本4和更新版本
* Safari 4版和更新版本
* Internet Explorer：

   * Windows 7和更新版本上的9+
   * Windows XP上的10+版

* Chrome 26版和更新版本

  >[!IMPORTANT]
  >
  >不支援Windows XP和Windows Vista上的Chrome Pepper。
