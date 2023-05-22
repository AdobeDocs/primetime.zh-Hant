---
description: 您可以通過將瀏覽器TVSDK與Adobe Analytics整合來跟蹤視頻使用情況。
title: 視頻分析
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 視頻分析{#video-analytics}

您可以通過將瀏覽器TVSDK與Adobe Analytics整合來跟蹤視頻使用情況。

瀏覽器中的視頻跟蹤TVSDK使用 **Adobe Analytics視頻軟體** 服務，它提供視頻接洽度量，如視頻視圖、視頻完成、廣告印象、視頻花費的時間等。 有關此服務的詳細資訊，請與Adobe代表聯繫。

以下過程匯總了在播放器中激活視頻跟蹤的步驟：

1. 初始化和/或配置以下視頻跟蹤元件：

   * **AppMeasurement庫**  — 包含低級資料收集核心邏輯。 這是通過網路累積和發送視頻心跳資料的地方。
   * **視頻心跳庫**  — 包含視頻心跳資料收集核心邏輯。 視頻心跳庫訪問AppMeasurement庫API的子集。

      >[!TIP]
      >
      >你的應用不會直接與視頻心跳代碼交互。 相反，該應用使用瀏覽器TVSDK API來配置播放器的視頻跟蹤功能。

   * **訪問者ID庫**  — 唯一標識承載視頻播放器的網頁的訪問者。
   >[!IMPORTANT]
   >
   >瀏覽器TVSDK內置視頻跟蹤功能取決於正確配置的AppMeasurement實例。 跟蹤元素假定在配置和激活視頻跟蹤之前已實例化並配置了AppMeasurement庫。 瀏覽器TVSDK視頻跟蹤功能取決於AppMeasurement庫是否存在一個功能齊全且配置正確的實例。

1. 使用Adobe Analytics管理工具在伺服器端設定視頻分析報告。
