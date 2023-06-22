---
title: 一般使用報告
description: 一般使用報告
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
source-git-commit: a2181a8fd7334f19b8387a31c71527d4f689ab9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 一般使用報告 {#general-usage-reports}

帳戶IQ報表是基本的分析工具和報表，可讓您鑽研資料以加以隔離 [同類群組](/help/AccountIQ/product-concepts.md#segmet-def)、識別異常，並建構對您帳戶特性的瞭解。

「一般使用報告」頁面提供工具，讓您根據使用的帳戶裝置數、偵測到的IP和個別郵遞區號來劃分子群組量度。

<!--Divide the content in cohorts.

Content filters
device filters

segment and definition replicate to cohorts. Number of people and number of account that ......
content consumption.....-->

所有報表都是根據以下專案選取的目前區段： [區段和時間範圍](/help/AccountIQ/howto-select-segment-timeframe.md) 面板。 您可以微調您的選取範圍，並透過指定（裝置數、IP數和郵遞區號數）臨界值來進一步縮小選取範圍。 [快照概述 — 超過臨界值的帳戶](#snapshot-overview) 面板。

<!--To view General Usage Reports:

1. Select the desired MVPDs from the **MVPDs in Segment** option.

2. Select the desired programmer channels from the **Channels in Segment** Option.

3. Select an appropriate time frame from the **Granularity and time frame** option.

   Using the above options you have defined segments for your analysis. Based on your segment selection, following graphs and reports are displayed.

4. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in [Snapshot Overview - Accounts above thresholds](#snapshot-overview) widget/panel.-->

## AuthN確定/AuthZ確定/播放請求/不重複訂閱者 {#authn-authz-playreq-uniquesubs}

此處的折線圖可讓您檢視定義區段在選定時間範圍內，AuthN OK、AuthZ OK、Play Requests和Unique Subscribers的值隨時間的變更。

+++程式設計師 —  **AuthN確定/AuthZ確定/播放請求/不重複訂閱者**

![](assets/progr-line-graph-gu.png)


*圖：程式設計人員使用者的AuthN確定/AuthZ確定/播放請求/不重複訂閱者*


+++


+++MVPD- **AuthN確定/AuthZ確定/不重複訂閱者**

![](assets/mvpd-line-graph-gu.png)


*圖：MVPD使用者的AuthN確定/ AuthZ確定/不重複訂閱者*


+++

x軸表示目前時間範圍內的單位，而y軸表示該期間的基本訂閱者活動量度。 折線圖可讓您比較您在區段選取面板中選取之MVPD和色版訂閱者的下列值：

* **驗證正常**

   AuthN OK是成功的驗證數目。 如需詳細資訊和定義，請參閱 [產品概念：驗證確定](/help/AccountIQ/product-concepts.md#authn-ok-def).

* **AuthZ確定**

   AuthZ OK是成功的授權數目。 如需詳細資訊和定義，請參閱 [產品概念：AuthZ確定](/help/AccountIQ/product-concepts.md#authz-ok-def).

* **播放請求**

   Play requests是播放要求數目。 如需詳細資訊和定義，請參閱 [產品概念：播放要求](/help/AccountIQ/product-concepts.md#play-requests-def)

   >[!NOTE]
   >
   >MVPD使用者無法使用播放要求線圖。


* **不重複訂閱者**

   Unique subscribers是成功的不重複訂閱者的數目。 如需詳細資訊和定義，請參閱 [產品概念：不重複訂閱者](/help/AccountIQ/product-concepts.md#unique-subscriber-def)

   >[!NOTE]
   >
   >如果程式設計師使用AdobeTempPass （即免費預覽）是區段的一部分，則獨特訂閱者的總數也包含不重複裝置數量。

## 快照概述 — 超過臨界值的帳戶 {#snapshot-overview}

使用此額外的篩選器微調您的分析和報告，以設定各種使用臨界值。 一旦您透過選取所需的MVPD和管道來定義要分析的區段（或同類群組）後，您還可以使用下列篩選器來分析訂閱者的行為：

* 裝置數量臨界值

* IP數量臨界值

* 郵遞區號數量臨界值

當您更新中的臨界值時 [科目節段 — 根據選取的臨界值](#account-segments-basedon-segments) 面板中，您可在以下位置檢視影響：

* [每個帳戶的每週（或每月）裝置數](#devices-week-account)

* [每個帳戶的每週（或月）位置](#locations-week-account)

* [每個帳戶每週（或每月）的IP](#ip-week-account)

* [科目節段的歷史檢視](#account-segment-historical-view)

>[!NOTE]
>
>每個臨界值的預設值為4。 也就是說，「一般使用方式」頁面會顯示訂閱者使用四個（及四個以上）裝置的MVPD分析，這些裝置使用四個（及更多）不同地理位置及四個（及更多）不同郵遞區號的內容。

### 科目節段 — 根據選取的臨界值 {#account-segments-basedon-segments}

此 **科目節段 — 根據選取的臨界值** 面板提供設定裝置數、IP數和郵遞區號數臨界值（介於1到10之間）的選項。

圖表會顯示：

* 訂閱者帳戶的絕對數量，以及

* 該區段中的訂戶帳戶總數百分比，

   使用X個裝置、Y個IP和Z個郵遞區號來在某個時間範圍內使用（已定義區段的） MVPD的管道內容。

![](assets/select-thresholds.png)

## 每個帳戶的每週（或每月）裝置數 {#devices-week-account}

此 **條狀圖** 提供有關訂閱者如何使用其裝置存取內容方面的使用行為深入分析。

X軸會繪製「帳戶數」，而Y軸會繪製「裝置數」。 它會根據您為每個帳戶設定的裝置數臨界值，標籤在一週內使用特定裝置數之內容的訂戶帳戶的絕對數目。

![](assets/bar-gr-devices-w-acc.png)

當游標停留在橫條上（特定於裝置數）時，會出現一個標籤，提供有關使用每週這些許多裝置串流頻道內容的訂閱者帳戶數（以及區段中的訂閱者帳戶總數百分比）的資訊。

此圖表也會標籤下列專案：

* 紅線表示您所設定的臨界值。

* 綠色線條，標示訂閱者帳戶每週（或每月）使用的不同裝置平均數量。

您可以將臨界值等級與帳戶使用的不同裝置數每週平均數進行比較，以判斷共用等級。

此圖表也會讓您一窺使用超過設定臨界值之裝置數的訂戶帳號百分比。

環圈圖可協助您一目瞭然地判斷使用超過設定臨界值（在時間範圍內）之裝置的頻道內容之訂閱者帳戶的大小。

![](assets/donut-devices-w-acc.png)

## 每個帳戶的每週（或每月）位置數 {#locations-week-account}

按讚 [每個帳戶的每週（或每月）裝置數](#devices-week-account)，每帳戶每週（或每月）的位置量度可協助您分析不同位置的訂戶帳戶使用情形，以更密切地識別密碼共用。 X軸會繪製「帳戶數」，而Y軸會繪製「位置數」。

此量度與數量結合的結果 [每個帳戶的每週（或每月）裝置數](#devices-week-account) 和數量 [每個帳戶每週（或每月）的IP](#ip-week-account) 協助您更準確地判斷密碼共用例項；如此一來，真實的使用者就不會計算在內。

![](assets/graph-loc-week-acc.png)

定義區段並設定位置數量的臨界值後，您就可以從圖形中識別：

* 一週內從（特定） x個位置消費內容的訂閱者人數（和百分比）。

* 從超過臨界值的位置檢視內容的總訂戶帳戶百分比。

* 比較每週平均值（帳戶的不同位置數量）與臨界值。

## 每個帳戶每週（或每月）的IP {#ip-week-account}

類似於 [每個帳戶的每週（或每月）裝置數](#devices-week-account) 和 [每個帳戶的每週（或每月）位置數](#locations-week-account)，則 **每個帳戶每週IP數量** 量度可讓您更精確、更精細地分析密碼共用。

X軸會繪製「帳戶數」，而Y軸會繪製「IP數」。

![](assets/graph-ip-week-acc.png)

定義區段（透過選取MVPD和通道）並設定IP數目的臨界值後，您就可以從圖形中識別：

* 一週內從（特定） x個IP位址使用內容的訂閱者人數（和百分比）。

* 從超過臨界值的IP位址檢視內容的總訂戶帳戶百分比。

* 比較每週平均值（帳戶的不同IP數量）和臨界值。

## 科目節段 — 歷史檢視表 {#account-segment-historical-view}

「歷史檢視」長條圖可協助您比較不同時間範圍內的使用量度。 此外，它還會集體繪製各種使用量度，例如 [每個帳戶的每週（或每月）裝置數](#devices-week-account)， [每個帳戶的每週（或每月）位置數](#locations-week-account)、和 [每個帳戶每週（或每月）的IP](#ip-week-account).

* x軸繪製時間範圍，y軸繪制訂戶帳戶、裝置、位置和IP的數量。

* 橙色長條表示各種時間範圍內的區段。

* 折線圖會繪製下列變更： [每個帳戶的每週（或每月）裝置數](#devices-week-account)， [每個帳戶的每週（或每月）位置數](#locations-week-account)、和 [每個帳戶每週（或每月）的IP](#ip-week-account) 時間範圍內的值，根據臨界值。

![](assets/historical-view.png)

* 藍色長條表示在某個時間範圍內整個產業中的活躍訂閱者總數。

* 您可以選取特定的圖例，它們可以協助您縮放圖形。

![](assets/historical-view-total.png)

>[!MORELIKETHIS]
>
>* 瞭解如何透過一般使用報告中的篩選器，匯出所選區段中前1000名訂閱者的報告 [匯出前1000個帳戶](/help/AccountIQ/export-acc-information.md) 選項。

