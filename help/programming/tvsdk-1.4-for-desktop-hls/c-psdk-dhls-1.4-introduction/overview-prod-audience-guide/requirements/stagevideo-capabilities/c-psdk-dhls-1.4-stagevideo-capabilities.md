---
description: 在支援GPU（硬體）加速的裝置上，您可以使用flash.media.StageVideo物件，在裝置硬體上處理視訊。 StageVideo的可用性視您系統不同部分的版本和功能而定，包括Flash Player、視訊硬體、作業系統、驅動程式、瀏覽器、網路連線和檢視內容。
seo-description: 在支援GPU（硬體）加速的裝置上，您可以使用flash.media.StageVideo物件，在裝置硬體上處理視訊。 StageVideo的可用性視您系統不同部分的版本和功能而定，包括Flash Player、視訊硬體、作業系統、驅動程式、瀏覽器、網路連線和檢視內容。
seo-title: StageVideo功能與限制
title: StageVideo功能與限制
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 概述{#stagevideo-capabilities-and-restrictions-overview}

在支援GPU（硬體）加速的裝置上，您可以使用flash.media.StageVideo物件，在裝置硬體上處理視訊。 StageVideo的可用性視您系統不同部分的版本和功能而定，包括Flash Player、視訊硬體、作業系統、驅動程式、瀏覽器、網路連線和檢視內容。

`StageVideo`類別可讓您運用硬體加速功能，將視訊呈現在裝置的最高效能等級。 `StageVideo`的可用性和效能受以下因素影響：

* **硬體加速** -當有硬體加速時， `StageVideo` 在裝置硬體上處理視訊。當硬體加速無法使用時，`StageVideo`回應會視您執行的Flash版本而定：

   * *Flash 15和更新版本* -當硬體加速不提供時， `StageVideo` 就會退回軟體，您就不必做任何事。

      >[!TIP]
      >
      >當硬體加速不可用時，效能可能會顯著下降。

   * *Flash 14及舊版* -當硬體加速無法使用時，就 `StageVideo` 會無法使用。在瀏覽器或GPU不支援硬體加速或在Flash Player中關閉的小組組態中，使用TVSDK HLS堆疊的視訊顯示將會失敗。 在&#x200B;*HDS*&#x200B;管線中，您可以從`StageVideo`切換到在CPU中處理視頻的替代對象，如Video對象。

* **簡報內容** -在全螢幕檢視期間， `StageVideo` 一律可供使用，而效能將維持在裝置上可用的最高等級。當不檢視全螢幕時，視訊簡報會落在瀏覽器的內容下，使用瀏覽器的設定和功能。

* **wmode**  —— 在瀏覽器上下文中，設 `wmode` 定對效能至關重要。Adobe建議您將`wmode`設為`direct`，以確保在瀏覽器內容中發揮最佳效能。

   >[!NOTE]
   >
   >包含`wmode`、`StageVideo`和Flash的因素組合，會產生不同的功能和限制，視您的硬體執行速度以及您使用的Flash版本而定。

   * *Flash 15和更新版本* - `StageVideo` 提供所有可用的 `wmode` 設定。但是，如果將`wmode`設定為`direct`以外的設定，則效能會降低。

   * *Flash 14及舊版* -如果您設 `wmode` 定為非 `direct`Flash的設定，則 `StageVideo` 並非所有瀏覽器都提供。

