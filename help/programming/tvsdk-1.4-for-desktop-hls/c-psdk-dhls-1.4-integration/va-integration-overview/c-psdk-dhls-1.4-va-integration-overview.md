---
description: 您可以通過將TVSDK與Adobe Analytics整合來跟蹤視頻使用。
title: 視頻分析
exl-id: 02303511-2713-4974-ada7-6f50fc500325
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 視頻分析{#video-analytics}

您可以通過將TVSDK與Adobe Analytics整合來跟蹤視頻使用。

TVSDK中的視頻跟蹤使用 **Adobe Analytics視頻軟體** 服務，它提供視頻接洽度量，如視頻視圖、視頻完成、廣告印象、視頻花費的時間等。 有關此服務的詳細資訊，請與Adobe代表聯繫。

以下過程匯總了在播放器中激活視頻跟蹤的步驟：

1. 初始化和/或配置以下視頻跟蹤元件：

   * **AppMeasurement庫**  — 包含低級資料收集核心邏輯。 這是通過網路累積和發送視頻心跳資料的地方。
   * **視頻心跳庫**  — 包含視頻心跳資料收集核心邏輯。 視頻心跳庫訪問 `AppMeasurement` 庫API。

      >[!TIP]
      >
      >你的應用不會直接與視頻心跳代碼交互。 相反，該應用使用TVSDK API來配置播放器的視頻跟蹤功能。

   * **訪問者ID庫**  — 唯一標識承載視頻播放器的網頁的訪問者。
   >[!IMPORTANT]
   >
   >TVSDK內置視頻跟蹤功能取決於正確配置 `AppMeasurement` 實例。 跟蹤元素假定 `AppMeasurement` 在配置和激活視頻跟蹤之前，庫已進行實例化和配置。 TVSDK視頻跟蹤功能取決於是否存在一個完全功能且正確配置的 `AppMeasurement` 的下界。

1. 使用Adobe Analytics管理工具在伺服器端設定視頻分析報告。
