---
description: 在支援GPU（硬體）加速的裝置上，您可以使用flash.media.StageVideo物件，在裝置硬體上處理視訊。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視頻硬體、作業系統、驅動程式、瀏覽器、網路連接和查看上下文。
title: StageVideo功能與限制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 概述{#stagevideo-capabilities-and-restrictions-overview}

在支援GPU（硬體）加速的裝置上，您可以使用flash.media.StageVideo物件，在裝置硬體上處理視訊。 StageVideo的可用性取決於系統不同部分的版本和功能，包括Flash Player、視頻硬體、作業系統、驅動程式、瀏覽器、網路連接和查看上下文。

`StageVideo`類別可讓您運用硬體加速功能，將視訊呈現在裝置的最高效能等級。 `StageVideo`的可用性和效能受以下因素影響：

* **硬體加速** -當有硬體加速時， `StageVideo` 在裝置硬體上處理視訊。當硬體加速不可用時，`StageVideo`響應取決於您運行的Flash版本：

   * *Flash* 15和更新版本——當硬體加速不 `StageVideo` 可用時，會退回軟體，您不必做任何事。

      >[!TIP]
      >
      >當硬體加速不可用時，效能可能會顯著下降。

   * *Flash14和舊版* -當硬體加速不可用時，就 `StageVideo` 會無法使用。在瀏覽器或GPU不支援硬體加速或在Flash Player中關閉的小組組態中，使用TVSDK HLS堆疊的視訊顯示將會失敗。 在&#x200B;*HDS*&#x200B;管線中，您可以從`StageVideo`切換到在CPU中處理視頻的替代對象，如Video對象。

* **簡報內容** -在全螢幕檢視期間， `StageVideo` 一律可供使用，而效能將維持在裝置上可用的最高等級。當不檢視全螢幕時，視訊簡報會落在瀏覽器的內容下，使用瀏覽器的設定和功能。

* **wmode**  —— 在瀏覽器上下文中，設 `wmode` 定對效能至關重要。Adobe建議您將`wmode`設為`direct`，以確保在瀏覽器上下文中盡可能提供最佳效能。

   >[!NOTE]
   >
   >包含`wmode`、`StageVideo`和Flash的因素組合會產生不同的功能和限制，具體取決於硬體的運行速度和您使用的Flash版本。

   * *Flash15和更新版本* - `StageVideo` 提供所有可用的 `wmode` 設定。但是，如果將`wmode`設定為`direct`以外的設定，則效能會降低。

   * *Flash14和舊版* -如果您設 `wmode` 定的設定不是 `direct`，則不 `StageVideo` 適用於所有瀏覽器。

