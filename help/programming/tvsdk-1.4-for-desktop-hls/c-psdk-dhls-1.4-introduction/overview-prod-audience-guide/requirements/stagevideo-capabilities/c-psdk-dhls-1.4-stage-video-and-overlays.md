---
description: 您可以將HTML疊加與StageVideo一起在Flash顯示清單視頻平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo始終顯示在任何Flash顯示清單元素後面。
title: StageVideo和HTML疊加
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo和HTML疊加{#stagevideo-and-html-overlays}

您可以將HTML疊加與StageVideo一起在Flash顯示清單視頻平面中顯示UI元素。 此平面位於StageVideo平面上方，因此StageVideo始終顯示在任何Flash顯示清單元素後面。

HTML疊加是UI元素，可在Flash顯示平面中顯示由 `StageVideo` 在自己的飛機上。 在Flash15之前，當硬體加速不可用時，不能使用HTML疊加。 從Flash15開始，HTML疊加顯示 `StageVideo` 退回到軟體呈現。

>[!IMPORTANT]
>
>根據系統的功能，使用HTML疊加時，效能可能會降低到大或小的程度。

請考慮以下資訊：

* 在Flash Player15中：

   * 您可以使用HTML覆蓋功能來驗證硬體加速是否可用。
   * 要使用HTML疊加，請設定 `wmode` 至 `opaque`。

* 在Flash Player14中：

   * 當硬體加速可用時， `StageVideo` 位於Flash顯示清單下方，因此可以使用HTML疊加。
   * 當硬體加速不可用時，視頻會呈現在瀏覽器中所有其他元素之上，這會阻止使用HTML疊加。

以下是使用HTML疊加的瀏覽器最低要求 `StageVideo`:

* Firefox版本4及更高版本
* Safari版本4及更高版本
* Internet Explorer:

   * Windows 7及更高版本上的9+版
   * Windows XP上的10+版

* Chrome版本26及更高版本

   >[!IMPORTANT]
   >
   >不支援Windows XP和Windows Vista上的Chrome Pepper。
