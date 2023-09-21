---
description: 您可以整合TVSDK與Adobe Analytics以追蹤視訊使用情況。
title: 視訊分析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 視訊分析{#video-analytics}

您可以整合TVSDK與Adobe Analytics以追蹤視訊使用情況。

TVSDK中的視訊追蹤使用 **Adobe Analytics影片要點** 服務，提供視訊參與量度，例如視訊觀看次數、視訊完成次數、廣告曝光數、視訊逗留時間等。 如需此服務的詳細資訊，請聯絡您的Adobe代表。

下列程式總結列出在播放器中啟動視訊追蹤的步驟：

1. 初始化及/或設定下列視訊追蹤元件：

   * **AppMeasurement程式庫**  — 包含低階資料收集核心邏輯。 這是累積視訊心率資料並透過網路傳送的位置。
   * **視訊心率程式庫**  — 包含視訊心率資料收集核心邏輯。 視訊心率程式庫會存取 `AppMeasurement` 資料庫API。

     >[!TIP]
     >
     >您的應用程式不會直接與視訊心率程式碼互動。 應用程式而是會使用TVSDK API來設定播放器的視訊追蹤功能。

   * **VisitorID程式庫**  — 唯一識別託管視訊播放器之網頁的訪客。

   >[!IMPORTANT]
   >
   >TVSDK內建的視訊追蹤功能取決於正確設定的 `AppMeasurement` 執行個體。 追蹤元素假設 `AppMeasurement` 在設定和啟用視訊追蹤之前，程式庫已具現化和設定。 TVSDK視訊追蹤功能取決於 `AppMeasurement` 資料庫。

1. 使用Adobe Analytics管理工具在伺服器端設定視訊分析報告。
