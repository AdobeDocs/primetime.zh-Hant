---
description: 您可以搭配StageVideo使用HTML覆蓋圖，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo一律會顯示在任何Flash顯示清單元素後面。
title: StageVideo和HTML覆蓋圖
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo和HTML覆蓋圖{#stagevideo-and-html-overlays}

您可以搭配StageVideo使用HTML覆蓋圖，在Flash顯示清單視訊平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo一律會顯示在任何Flash顯示清單元素後面。

HTML覆蓋圖是UI元素，您可以在轉譯的視訊的Flash顯示平面中顯示 `StageVideo` 在它自己的平面上。 在Flash15之前，如果硬體加速不可用，則無法使用HTML覆蓋。 從Flash15開始，HTML覆蓋圖會在下列情況下顯示： `StageVideo` 退回至軟體轉譯。

>[!IMPORTANT]
>
>當您使用HTML覆蓋圖時，效能可能會或多或少地降低，這取決於您的系統功能。

請考量下列資訊：

* 在Flash Player15中：

   * 無論硬體加速是否可用，您都可以使用HTML覆蓋圖。
   * 若要使用HTML覆蓋圖，請設定 `wmode` 至 `opaque`.

* 在Flash Player14中：

   * 當硬體加速可用時， `StageVideo` 位在Flash顯示清單下方，因此您可以使用HTML覆蓋圖。
   * 無法使用硬體加速時，視訊會呈現至瀏覽器中所有其他元素上方，以防止使用HTML覆蓋圖。

以下為搭配使用HTML覆蓋圖的最低瀏覽器需求 `StageVideo`：

* Firefox版本4和更新版本
* Safari版本4和更新版本
* Internet Explorer：

   * Windows 7及更新版本上的9+
   * Windows XP上的10+版

* Chrome 26版和更新版本

   >[!IMPORTANT]
   >
   >不支援Windows XP和Windows Vista上的Chrome Pepper。
