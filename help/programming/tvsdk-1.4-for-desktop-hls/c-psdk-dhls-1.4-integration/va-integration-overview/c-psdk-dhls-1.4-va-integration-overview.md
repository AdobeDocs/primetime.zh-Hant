---
description: 您可以整合TVSDK與Adobe Analytics以追蹤視訊使用情況。
title: 視訊分析
exl-id: 02303511-2713-4974-ada7-6f50fc500325
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 視訊分析{#video-analytics}

您可以整合TVSDK與Adobe Analytics以追蹤視訊使用情況。

TVSDK中的視訊追蹤會使用 **Adobe Analytics Video Essentials** 此服務提供視訊參與量度，例如視訊觀看次數、視訊完成次數、廣告曝光數、視訊逗留時間等。 如需此服務的詳細資訊，請聯絡您的Adobe代表。

下列程式總結列出在播放器中啟動視訊追蹤的步驟：

1. 初始化及/或設定下列視訊追蹤元件：

   * **AppMeasurement資料庫**  — 包含低階資料收集核心邏輯。 這是累積視訊心率資料並透過網路傳送的位置。
   * **視訊心率資料庫**  — 包含視訊心率資料收集核心邏輯。 視訊心率程式庫會存取 `AppMeasurement` 資料庫API。

      >[!TIP]
      >
      >您的應用程式不會直接與視訊心率程式碼互動。 應用程式會改用TVSDK API來設定播放器的視訊追蹤功能。

   * **VisitorID程式庫**  — 唯一識別託管視訊播放器之網頁的訪客。
   >[!IMPORTANT]
   >
   >TVSDK內建的視訊追蹤功能取決於正確設定的 `AppMeasurement` 執行個體。 追蹤元素會假設 `AppMeasurement` 在設定和啟用視訊追蹤之前，程式庫已具現化和設定。 TVSDK視訊追蹤功能取決於 `AppMeasurement` 資料庫。

1. 使用Adobe Analytics管理工具在伺服器端設定視訊分析報告。
