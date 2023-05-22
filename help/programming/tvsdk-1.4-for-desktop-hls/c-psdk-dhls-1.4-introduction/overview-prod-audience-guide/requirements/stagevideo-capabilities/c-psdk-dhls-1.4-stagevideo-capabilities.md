---
description: 在支援GPU（硬體）加速的設備上，可以使用flash.media.StageVideo對象在設備硬體上處理視頻。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視頻硬體、作業系統、驅動程式、瀏覽器、網路連接和查看上下文。
title: StageVideo功能和限制
exl-id: 228ea2d0-5950-43f5-8cfd-640d1c482b05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概述 {#stagevideo-capabilities-and-restrictions-overview}

在支援GPU（硬體）加速的設備上，可以使用flash.media.StageVideo對象在設備硬體上處理視頻。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視頻硬體、作業系統、驅動程式、瀏覽器、網路連接和查看上下文。

的 `StageVideo` 類允許您利用硬體加速功能以設備的最高效能級別呈現視頻。 可用性和效能 `StageVideo` 受以下因素影響：

* **硬體加速**  — 當硬體加速可用時， `StageVideo` 在設備硬體上處理視頻。 當硬體加速不可用時， `StageVideo` 響應取決於您正在運行的Flash版本：

   * *Flash15及更高版本*  — 當硬體加速不可用時， `StageVideo` 退回到軟體，你什麼都不用做。

      >[!TIP]
      >
      >當硬體加速不可用時，效能可能會顯著下降。

   * *Flash14及更早版本*  — 當硬體加速不可用時， `StageVideo` 變得不可用。 在瀏覽器或GPU不支援硬體加速或Flash Player中關閉的一組小配置中，TVSDK HLS堆棧的視頻顯示將失敗。 在 *HDS* 管道，可從 `StageVideo` 到在CPU中處理視頻的備選對象，如Video對象。

* **演示上下文**  — 在全屏查看期間， `StageVideo` 始終可用，並且效能將處於設備上可用的最高級別。 當不全屏查看時，視頻演示文稿位於瀏覽器的上下文下，其中使用了瀏覽器的設定和功能。

* **wmode（w模式）**  — 在瀏覽器上下文中， `wmode` 設定對效能至關重要。 Adobe建議您 `wmode` 設定為 `direct` 確保瀏覽器上下文中的最佳效能。

   >[!NOTE]
   >
   >包括以下因素的組合 `wmode`。 `StageVideo`，並且Flash會導致不同的功能和限制，具體取決於硬體運行的速度以及您使用的Flash版本。

   * *Flash15及更高版本* - `StageVideo` 所有可用 `wmode` 的子菜單。 但是，如果 `wmode` 設定 `direct`，效能會降低。

   * *Flash14及更早版本*  — 如果設定 `wmode` 設定 `direct`。 `StageVideo` 在所有瀏覽器中均不可用。
