---
title: 常規使用情況報告
description: 常規使用情況報告
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
source-git-commit: a2181a8fd7334f19b8387a31c71527d4f689ab9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 常規使用情況報告 {#general-usage-reports}

帳戶IQ報告是基本的分析工具和報告，使您能夠深入查看資料以隔離 [馬蹄](/help/AccountIQ/product-concepts.md#segmet-def)、識別異常，並瞭解您的客戶特性。

「一般使用情況報告」頁提供了根據使用中的帳戶設備數、檢測到的IP和相應的郵遞區號劃分子組度量的工具。

<!--Divide the content in cohorts.

Content filters
device filters

segment and definition replicate to cohorts. Number of people and number of account that ......
content consumption.....-->

所有報告均基於使用 [段和時間框架](/help/AccountIQ/howto-select-segment-timeframe.md) 的子菜單。 您可以通過在中指定（設備數、 IP數和郵遞區號數）閾值來微調您的選擇並進一步縮小選擇範圍 [快照概述 — 超過閾值的帳戶](#snapshot-overview) 的子菜單。

<!--To view General Usage Reports:

1. Select the desired MVPDs from the **MVPDs in Segment** option.

2. Select the desired programmer channels from the **Channels in Segment** Option.

3. Select an appropriate time frame from the **Granularity and time frame** option.

   Using the above options you have defined segments for your analysis. Based on your segment selection, following graphs and reports are displayed.

4. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in [Snapshot Overview - Accounts above thresholds](#snapshot-overview) widget/panel.-->

## AuthN OK / AuthZ OK /播放請求/唯一訂閱者 {#authn-authz-playreq-uniquesubs}

此處的折線圖為您提供了定義段的選定時間範圍內AuthN OK 、 AuthZ OK 、 Play Requests和Unique Subscribers值隨時間變化的視圖。

+++程式設計師 —  **AuthN OK / AuthZ OK /播放請求/唯一訂閱者**

![](assets/progr-line-graph-gu.png)


*圖：針對程式設計師用戶的AuthN OK / AuthZ OK / Play Requests /唯一訂閱者*


+++


+++MVPD- **AuthN OK / AuthZ OK /唯一訂閱者**

![](assets/mvpd-line-graph-gu.png)


*圖：AuthN OK / AuthZ OK / MVPD用戶的唯一訂閱者*


+++

x軸表示當前時間範圍內的單位，y軸表示該時段內的基本訂戶活動度量。 通過線形圖，您可以比較在段選擇面板中選擇的MVPD和通道的訂戶的以下值：

* **AuthN確定**

   AuthN OK是成功身份驗證的次數。 有關詳細資訊和定義，請參閱 [產品概念：AuthN確定](/help/AccountIQ/product-concepts.md#authn-ok-def)。

* **AuthZ確定**

   AuthZ OK是成功的授權數。 有關詳細資訊和定義，請參閱 [產品概念：AuthZ確定](/help/AccountIQ/product-concepts.md#authz-ok-def)。

* **播放請求**

   播放請求是播放請求數。 有關詳細資訊和定義，請參閱 [產品概念：播放請求](/help/AccountIQ/product-concepts.md#play-requests-def)

   >[!NOTE]
   >
   >播放請求線形圖對MVPD用戶不可用。


* **唯一訂閱者**

   Unique預訂者是成功的唯一預訂者數。 有關詳細資訊和定義，請參閱 [產品概念：唯一訂閱者](/help/AccountIQ/product-concepts.md#unique-subscriber-def)

   >[!NOTE]
   >
   >如果程式設計師使用AdobeTempPass（即免費預覽）是段的一部分，則唯一訂閱者總數還包括唯一設備數。

## 快照概述 — 超過閾值的帳戶 {#snapshot-overview}

使用此附加篩選器微調分析和報告以設定各種使用閾值。 一旦通過選擇所需的MVPD和通道來定義要分析的段（或隊列），您還可以使用以下篩選器來分析訂閱者行為：

* 設備數閾值

* IP數閾值

* 郵遞區號閾值數

在中更新閾值時 [帳戶段 — 基於選定閾值](#account-segments-basedon-segments) 面板中，您可以在中查看影響：

* [每個帳戶每週（或每月）的設備](#devices-week-account)

* [每個帳戶每週（或每月）的位置](#locations-week-account)

* [每個帳戶每週（或每月）的IP](#ip-week-account)

* [帳戶段的歷史視圖](#account-segment-historical-view)

>[!NOTE]
>
>每個閾值的預設值為4。 也就是說，「一般用法」頁顯示MVPD的分析，訂戶使用四台（和四台以上）設備，從四個（或更多）不同地理位置和四個（或更多）不同的郵遞區號消耗內容。

### 帳戶段 — 基於選定閾值 {#account-segments-basedon-segments}

的 **帳戶段 — 基於選定閾值** 面板為您提供了設定設備數、IP數和郵遞區號數的閾值（介於1和10之間）的選項。

該圖表顯示：

* 訂戶帳戶的絕對數，以及

* 佔該段的訂戶帳戶總數的百分比，

   使用X個設備、Y個IP和Z個Z個Zip代碼，在一段時間內從您的渠道為（定義的）MVPD消耗內容。

![](assets/select-thresholds.png)

## 每個帳戶每週（或每月）的設備 {#devices-week-account}

的 **條形圖** 提供關於訂閱者如何使用其設備訪問內容的使用行為的見解。

x軸以「帳戶數」為圖表，y軸以「設備數」為圖表。 根據為每個帳戶設定的設備數設定的閾值，它標籤在一週的持續時間內從特定數量的設備消耗內容的訂戶帳戶的絕對數量。

![](assets/bar-gr-devices-w-acc.png)

當懸停在條形（特定於設備數）上時，將顯示一個標籤，該標籤提供有關一週內使用這些許多設備流式傳輸頻道內容的訂戶帳戶數（以及段中訂戶帳戶總數的百分比）的資訊。

該圖還標籤以下內容：

* 用於標籤所設定的閾值的紅線。

* 用於標籤訂閱者帳戶每週（或月）使用的不同設備的平均數的綠線。

您可以將閾值級別與帳戶使用的不同設備的每週平均數量進行比較，以判斷共用級別。

該圖表還提供了使用比設定閾值更多設備的訂戶帳戶的百分比。

甜圈圖可幫助您一眼就判斷使用超過設定閾值（時間段內）的設備消耗頻道內容的用戶帳戶的數量。

![](assets/donut-devices-w-acc.png)

## 每個帳戶每週（或每月）的位置 {#locations-week-account}

像 [每個帳戶每週（或每月）的設備](#devices-week-account)，每週（或每月）的「帳戶位置」度量可幫助您分析不同位置的訂戶帳戶使用情況，以更密切地識別密碼共用。 x軸以「帳戶數」(Number of Accounts)為圖表，y軸以「位置數」(Number of Locations)為圖表。

此度量的結果與 [每個帳戶每週（或每月）的設備](#devices-week-account) 和數量 [每個帳戶每週（或每月）的IP](#ip-week-account) 幫助您更準確地判斷密碼共用實例；這樣，真實用戶就不被計算在內。

![](assets/graph-loc-week-acc.png)

定義了段並設定了位置數的閾值後，可以從圖形中標識：

* 在一週內從（特定）x個位置消費內容的訂戶數（和百分比）。

* 從超過閾值的位置查看內容的訂戶帳戶總數的百分比。

* 將每週平均值（帳戶的不同位置數）與閾值進行比較。

## 每個帳戶每週（或每月）的IP {#ip-week-account}

類似於 [每個帳戶每週（或每月）的設備](#devices-week-account) 和 [每個帳戶每週（或每月）的位置](#locations-week-account)，也請參見Wiki頁。 **每個帳戶每週的IP數** 度量允許您更精確、更精細地分析密碼共用。

x軸以圖表示帳戶數，y軸以圖表示IP數。

![](assets/graph-ip-week-acc.png)

定義段（通過選擇MVPD和通道）並設定IP數的閾值後，可以從圖表中標識：

* 在一週內從（特定）x IP數量消耗內容的訂戶數（和百分比）。

* 從多於閾值的IP地址查看內容的訂戶帳戶總數的百分比。

* 將每週平均值（帳戶的不同IP數）與閾值進行比較。

## 帳戶段 — 歷史視圖 {#account-segment-historical-view}

「歷史視圖」條形圖可幫助您比較不同時間幀的使用度量。 此外，它會以集合形式繪製各種使用度量，如 [每個帳戶每週（或每月）的設備](#devices-week-account)。 [每個帳戶每週（或每月）的位置](#locations-week-account), [每個帳戶每週（或每月）的IP](#ip-week-account)。

* x軸以圖表方式顯示時間幀，y軸以圖表方式顯示訂戶帳戶、設備、位置和IP的數量。

* 橙色色條表示不同時間幀中的段。

* 線形圖以曲線圖顯示 [每個帳戶每週（或每月）的設備](#devices-week-account)。 [每個帳戶每週（或每月）的位置](#locations-week-account), [每個帳戶每週（或每月）的IP](#ip-week-account) 根據閾值跨時間幀的值。

![](assets/historical-view.png)

* 藍條表示整個行業內一段時間內的活動用戶總數。

* 您可以選擇特定的圖例，這些圖例將幫助您縮放圖形。

![](assets/historical-view-total.png)

>[!MORELIKETHIS]
>
>* 瞭解如何使用常規使用情況報告中的篩選器導出所選段中前1000名訂閱者的報告 [導出前1000個帳戶](/help/AccountIQ/export-acc-information.md) 的雙曲餘切值。

