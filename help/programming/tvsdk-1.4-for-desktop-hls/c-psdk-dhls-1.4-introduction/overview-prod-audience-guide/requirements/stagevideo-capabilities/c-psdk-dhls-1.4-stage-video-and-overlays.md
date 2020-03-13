---
description: 您可搭配StageVideo使用HTML覆蓋，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo一律會顯示在任何Flash顯示清單元素後方。
seo-description: 您可搭配StageVideo使用HTML覆蓋，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo一律會顯示在任何Flash顯示清單元素後方。
seo-title: StageVideo和HTML覆蓋
title: StageVideo和HTML覆蓋
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo和HTML覆蓋{#stagevideo-and-html-overlays}

您可搭配StageVideo使用HTML覆蓋，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo一律會顯示在任何Flash顯示清單元素後方。

HTML覆蓋是UI元素，您可在Flash顯示平面中，在視訊上顯示，而視訊則由視訊在 `StageVideo` 其自己的平面上呈現。 在Flash 15之前，當硬體加速無法使用時，您無法使用HTML覆蓋。 從Flash 15開始，當回到軟體演算時，會 `StageVideo` 顯示HTML覆蓋。

>[!IMPORTANT]
>
>視您系統的功能而定，當您使用HTML覆蓋時，效能可能會降低至較大或較小。

請考慮下列資訊：

* 在Flash Player 15中：

   * 無論硬體加速是否可用，您都可以使用HTML覆蓋。
   * 若要使用HTML覆蓋，請設 `wmode` 為 `opaque`。

* 在Flash Player 14中：

   * 當硬體加速可用時， `StageVideo` 位於Flash顯示清單下方，因此您可以使用HTML覆蓋。
   * 當無法使用硬體加速時，視訊會呈現在瀏覽器中所有其他元素的上方，以防止使用HTML覆蓋。

以下是搭配使用HTML覆蓋的最低瀏覽器需求 `StageVideo`:

* Firefox 4和更新版本
* Safari 4和更新版本
* Internet Explorer:

   * Windows 7和更新版本上的9+版
   * Windows XP上的10+版

* Chrome 26及更新版本

   >[!IMPORTANT]
   >
   >Windows XP和Windows Vista上不支援Chrome Pepper。

