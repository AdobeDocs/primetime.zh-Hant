---
title: 共用帳戶報表
description: 共用帳戶報表
exl-id: 16c5ded1-2a95-4373-8b90-b445131f333a
source-git-commit: dd1001d94e32a1a8b5346ff97b0f6cb7d244dcf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 共用帳戶報表 {#shared-accounts-reports}

「共用帳戶報表」會依選取的共用機率範圍來劃分量度，例如裝置數量和裝置類型 **超過中等概率** 和 **機率過低** （針對目前區段）。

然後，這些範圍可作為用戶定義的閾值，並且圖形會根據所選閾值進行更新。

帳戶IQ會根據已定義區段的所有訂閱者帳戶的共用機率，依下列五個類別將其分類為帳戶：

* 非常高(80%-100%)
* 高(60%-80%)
* 適中(40%-60%)
* 低(20%-40%)
* 非常低(0%-20%)

## 帳戶共用機率 {#accounts-sharing-probability}

此處的環圈圖按不同概率類別分類並顯示訂戶帳戶的百分比（和絕對數）。

紅線會標籤使用者在 [當前段中超過閾值的帳戶](#threshold-selector) 中。

![](assets/accounts-sharing-probability-pie.png)

長條圖繪製各類共用概率的Y軸帳戶數（在X軸上繪製）。

![](assets/accounts-sharing-probability-bar.png)

紅線會標籤臨界值範圍，並可在長條圖中調整。 在長條圖中調整的臨界值反映在環圈圖中的臨界值範圍。

<!--![](assets/shared-accounts-rep.gif)-->

### 當前段中超過閾值的帳戶{#threshold-selector}

此面板可讓您選取以下範圍作為訂閱者帳戶的臨界值（根據其分享機率）:

* 帳戶 **非常低** 共用 **概率**

* 帳戶 **過低** 共用 **概率**

* 帳戶 **審核** 共用 **概率**

* 帳戶 **過高** 共用 **概率**

![](assets/threshold-selector-shared-accounts.png)

選取臨界值後，面板會顯示所選區段中所有訂閱者帳戶的帳戶百分比（和數目）。

## 區段 — 從總計播放請求 {#play-request-out-total}

環圈圖顯示訂閱者在區段中提出的播放請求百分比（和數目）;和可讓您比較未在定義區段中訂閱者提出的播放請求。

![](assets/play-req-outof-total.png)

當您在環圈圖上移動游標時，它還顯示訂閱者百分比和來自各種概率範圍的數字。

<!--![](assets/play-request-total.gif)-->

## 每個帳戶的平均裝置數量{#avg-devices-account}

長條圖顯示目前區段中的訂閱者和目前區段以外的訂閱者，正在使用之每種裝置類型的平均裝置數量。

![](assets/avg-devices-per-acc.png)

## 區段 — 每個帳戶的每個期間的郵遞區號 {#zip-codes-period-account}

此圖表會通知您某個時間範圍內，從不同位置使用內容的訂閱者人數。

![](assets/zip-period-account.png)

您可以放大，縮小並檢視圖表中繪製位置範圍的長條的細節。

<!--![](assets/zip-code-period.gif)-->

## 分部 — 地理範圍/期間/帳戶 {#geo-span-period-account}

此長條圖以英里為單位繪製與不同地理範圍範圍相關的訂戶帳戶數。 該範圍基於用戶在時間幀期間已經流式傳輸的位置之間的最大距離。

<!--Total number of users ...

How many accounts are within 99 miles of each other.....and how many are apart. 

Based on points on the map.-->

![](assets/geogr-span-account.png)

當您選取代表地理距離範圍的長條時，長條會展開範圍以顯示更多詳細資料。

<!--![](assets/geo-span-period-acc.gif)-->
