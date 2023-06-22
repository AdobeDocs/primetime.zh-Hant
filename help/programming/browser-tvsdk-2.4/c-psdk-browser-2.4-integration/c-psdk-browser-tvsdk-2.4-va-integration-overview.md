---
description: 您可以將瀏覽器TVSDK與Adobe Analytics整合，以追蹤視訊使用情形。
title: 視訊分析
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 視訊分析{#video-analytics}

您可以將瀏覽器TVSDK與Adobe Analytics整合，以追蹤視訊使用情形。

瀏覽器TVSDK中的視訊追蹤會使用 **Adobe Analytics Video Essentials** 此服務提供視訊參與量度，例如視訊觀看次數、視訊完成次數、廣告曝光數、視訊逗留時間等。 如需此服務的詳細資訊，請聯絡您的Adobe代表。

下列程式總結列出在播放器中啟動視訊追蹤的步驟：

1. 初始化及/或設定下列視訊追蹤元件：

   * **AppMeasurement資料庫**  — 包含低階資料收集核心邏輯。 這是累積視訊心率資料並透過網路傳送的位置。
   * **視訊心率資料庫**  — 包含視訊心率資料收集核心邏輯。 視訊心率程式庫會存取AppMeasurement程式庫API的子集。

      >[!TIP]
      >
      >您的應用程式不會直接與視訊心率程式碼互動。 應用程式會改用瀏覽器TVSDK API來設定播放器的視訊追蹤功能。

   * **VisitorID程式庫**  — 唯一識別託管視訊播放器之網頁的訪客。
   >[!IMPORTANT]
   >
   >瀏覽器TVSDK內建的視訊追蹤功能取決於正確設定的AppMeasurement例項。 追蹤元素假設在設定和啟用視訊追蹤之前，AppMeasurement程式庫已具現化並完成設定。 瀏覽器TVSDK視訊追蹤功能取決於AppMeasurement程式庫是否存在功能齊全且設定正確的執行個體。

1. 使用Adobe Analytics管理工具在伺服器端設定視訊分析報告。
