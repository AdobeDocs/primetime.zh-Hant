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

「共用帳戶報表」會依選取的共用機率範圍來劃分度量，例如裝置和裝置型別的數目 **超過中度機率** 和 **超低機率** 用於目前區段。

然後，這些範圍可作為使用者定義的臨界值，且圖表會根據選取的臨界值更新。

科目IQ會根據科目共用的機率，將已定義節段的所有訂閱者科目分類為具有下列五個類別的科目：

* 非常高(80%-100%)
* 高(60%-80%)
* 中度(40%-60%)
* 低(20%-40%)
* 非常低(0%-20%)

## 帳戶共用機率 {#accounts-sharing-probability}

此處的環圈圖會分類並顯示來自各種機率類別的訂閱者帳號百分比（和絕對數字）。

紅線會標籤使用者在中選取的臨界值範圍 [目前區段中的帳戶超過臨界值](#threshold-selector) 面板。

![](assets/accounts-sharing-probability-pie.png)

長條圖在Y軸上繪製各種共用機率類別的帳戶數（繪製在X軸上）。

![](assets/accounts-sharing-probability-bar.png)

紅線會標籤臨界值的範圍，並可在長條圖中進行調整。 在長條圖中調整的臨界值會反映在環形圖的臨界值範圍內。

<!--![](assets/shared-accounts-rep.gif)-->

### 目前區段中的帳戶超過臨界值{#threshold-selector}

此面板可讓您從下列範圍中選取一個範圍，作為訂戶帳戶的臨界值（根據其共用機率）：

* 帳戶 **非常低** 共用 **機率**

* 帳戶 **過低** 共用 **機率**

* 帳戶 **超過稽核** 共用 **機率**

* 帳戶 **過高** 共用 **機率**

![](assets/threshold-selector-shared-accounts.png)

選取臨界值後，面板會顯示所選區段中所有訂戶帳戶的帳戶百分比（和數目）。

## 區段 — 播放請求總計 {#play-request-out-total}

環形圖顯示區段中訂閱者提出的播放要求百分比（和數量），並可讓您比較不在定義區段中的訂閱者提出的播放要求。

![](assets/play-req-outof-total.png)

當您在環圈圖上移動游標時，它也會顯示來自各種機率範圍的訂戶百分比和數字。

<!--![](assets/play-request-total.gif)-->

## Segment — 每個帳戶的平均裝置數{#avg-devices-account}

長條圖顯示目前區段中的訂閱者和目前區段以外的訂閱者所使用的每種裝置型別的平均裝置數。

![](assets/avg-devices-per-acc.png)

## 區段 — 每個帳戶每個期間的郵遞區號 {#zip-codes-period-account}

此圖表會通知您在一個時間範圍內從不同位置使用內容的訂閱者人數。

![](assets/zip-period-account.png)

您可以放大以縮小並檢檢視形中某條的具體資訊，該圖形繪製了一系列位置。

<!--![](assets/zip-code-period.gif)-->

## 區段 — 地理範圍/期間/帳戶 {#geo-span-period-account}

此長條圖會根據不同地理範圍範圍（以英里為單位）繪制訂閱者帳戶數量。 此範圍是以時間範圍內訂閱者已串流過的位置之間的最大距離為基礎。

<!--Total number of users ...

How many accounts are within 99 miles of each other.....and how many are apart. 

Based on points on the map.-->

![](assets/geogr-span-account.png)

當您選取代表某個地理距離範圍的長條時，它會展開該範圍以顯示更多詳細資訊。

<!--![](assets/geo-span-period-acc.gif)-->
