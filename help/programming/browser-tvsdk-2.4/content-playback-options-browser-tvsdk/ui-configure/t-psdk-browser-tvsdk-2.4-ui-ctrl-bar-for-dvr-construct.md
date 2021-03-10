---
description: 您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。
title: 構建用於DVR的增強控制條
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 構建增強的DVR控制條{#construct-a-control-bar-enhanced-for-dvr}

您可以實作具有VOD和即時串流DVR支援的控制列。 DVR支援包括可檢視視窗和用戶端即時點的概念。

* 對於VOD，可檢視視窗的長度是整個資產的期間。
* 對於即時串流，DVR（可設定）視窗的長度會定義為從即時播放視窗開始到用戶端即時點結束的時間範圍。

   用戶端即時點是透過從即時視窗端減去緩衝長度來計算。 目標持續時間是大於或等於清單中片段的最大持續時間的值。

   用於即時回放的控制條通過首先在開始回放時將拇指定位在客戶端即時點以及通過顯示標籤不允許搜索的區域來支援DVR。

對於控制列：

1. 新增覆蓋至代表播放範圍的控制列。

1. 當使用者開始搜尋時，檢查所要的搜尋位置是否在可搜尋範圍內。
