---
description: 在支援GPU （硬體）加速的裝置上，您可以使用flash.media.StageVideo物件來處理裝置硬體上的視訊。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視訊硬體、作業系統、驅動程式、瀏覽器、網路連線以及檢視內容。
title: StageVideo功能和限制
exl-id: 228ea2d0-5950-43f5-8cfd-640d1c482b05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概觀 {#stagevideo-capabilities-and-restrictions-overview}

在支援GPU （硬體）加速的裝置上，您可以使用flash.media.StageVideo物件來處理裝置硬體上的視訊。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視訊硬體、作業系統、驅動程式、瀏覽器、網路連線以及檢視內容。

此 `StageVideo` 類別可讓您利用硬體加速，以裝置的最高效能等級呈現視訊。 的可用性與效能 `StageVideo` 會受到下列因素的影響：

* **硬體加速**  — 可使用硬體加速時， `StageVideo` 在裝置硬體上處理視訊。 硬體加速不可用時， `StageVideo` 回應取決於您執行的Flash版本：

   * *Flash15和更新版本*  — 無法使用硬體加速時， `StageVideo` 回到軟體，您不必執行任何動作。

      >[!TIP]
      >
      >當無法使用硬體加速時，效能可能會大幅降低。

   * *Flash14及舊版*  — 無法使用硬體加速時， `StageVideo` 會變成無法使用。 在瀏覽器或GPU不支援硬體加速或在Flash Player中關閉的少數設定中，使用TVSDK HLS棧疊的視訊顯示將會失敗。 在 *HDS* 管道，您可以從 `StageVideo` 變更為替代物件（例如Video物件），會在CPU中處理視訊。

* **簡報內容**  — 全熒幕檢視期間， `StageVideo` 永遠可用，而且效能會保持在裝置上可用的最高等級。 當未以全熒幕檢視時，視訊簡報會落在瀏覽器的上下文下，而此上下文會使用瀏覽器的設定和功能。

* **wmode**  — 在瀏覽器內容中， `wmode` 設定對效能至關重要。 Adobe建議您保留 `wmode` 設定為 `direct` 以確保在瀏覽器內容中達到最佳效能。

   >[!NOTE]
   >
   >這些因素包括 `wmode`， `StageVideo`和的Flash會產生不同的功能和限制，具體取決於硬體執行速度和使用的Flash版本。

   * *Flash15和更新版本* - `StageVideo` 隨所有可用專案提供 `wmode` 設定。 不過，如果您設定 `wmode` 至以外的設定 `direct`，效能將會較低。

   * *Flash14及舊版*  — 如果您設定 `wmode` 至以外的設定 `direct`， `StageVideo` 並非所有瀏覽器都提供。
