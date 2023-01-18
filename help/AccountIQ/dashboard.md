---
title: 帳戶IQ控制面板
description: 控制面板可協助您分析廣泛的訂閱者資料，以找出密碼共用的例項。
exl-id: 616da2a5-c9fe-40ea-90cf-f565bc13e764
source-git-commit: a2181a8fd7334f19b8387a31c71527d4f689ab9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# 控制面板 {#dashboard}

控制面板會摘要並匯總圖表和報表的集合中的資料，這些圖表和報表旨在提供帳戶共用的範圍和影響的概觀。 它提供單一頁面，內含帳戶IQ的主要報表和量度。


+++程式設計師 — 儀表板

![面向程式設計師用戶的帳戶IQ儀表板](assets/dashboard-programr.png)


圖：面向程式設計師用戶的儀表板

+++

+++MVPD — 控制面板

MVPD用戶的儀表板與程式設計師用戶的儀表板稍有不同。

![面向程式設計師用戶的帳戶IQ儀表板](assets/dashboard-mvpd.png)

圖：MVPD使用者的控制面板

+++

## 平均共用分數 — 匯總目前區段 {#aggregated-sharing}

「匯總共用分數」面板提供頂線讀出，匯總以帳戶和流量表示的共用數量和影響。

這些值有助於您了解訂閱者共用憑證的規模，從而提供對此採取行動的必要性的度量。

![](assets/aggregate-sharing-score.png)


*圖：平均共用分數面板 — 匯總為目前區段*

以下三個量度是「平均共用分數」的元件。

### 共用層級 {#sharing-level}

共用等級量規會顯示在所選時間範圍內共用的所有訂閱者帳戶（在定義的區段中）的百分比。

根據在所選時間幀期間從一個所選節目編寫器通道流傳送的選定MVPD集合中每個帳戶的共用概率的平均值計算的值。

![](assets/sharing-level.png)


*圖：共用層級*

趨勢指標會顯示中度量值與上一個時間範圍相比的百分比變更。

### 來自共用帳戶的使用 {#usage-from-shared-accounts}

此量規指示所有訂閱者帳戶的使用百分比來自定義的段和時段的共用帳戶。 量規會將使用範圍（從共用帳戶）標示為0到100%。 這些範圍（稱為低、中、高和異常）均基於行業平均值。

您也可以看到趨勢指標，與上一個時間範圍相比，該指標描繪來自共用帳戶的使用量增加或減少。

![](assets/usage-4mshared-accounts.png)


*圖：來自共用帳戶的使用*

### 整體共用分數 {#overall-sharing-score}

整體共用分數是共用分數的組合，包括「共用層級」和「共用帳戶的使用情況」。

它提供的值旨在反映與業界相比共用的相對影響。 目的與信用評分相似，用單一數字來總結情況。 但在這種情況下，數字越高，潛在危害就越大。

![](assets/overall-sharing-score.png)


*圖：整體共用分數*

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)-->

## MVPD的全行業整體共用分數 {#top-mvpds}

下表提供區段中MVPD之不同匯總共用分數的比較檢視。

>[!NOTE]
>
>此表格使用整體產業資料進行比較，而非區段中由這些MVPD所代表的資料。

![](assets/top-mvpds.png)


*圖：依整體分數劃分的區段中排名最前的MVPD*

## 依頻道和MVPD共用分數 {#sharin-score-by-channels-and-mvpds}

下表提供目前區段中，MVPD所選管道的共用分數比較檢視。

![](assets/sharing-scores-by-channels-mvpds.png)


*圖：依頻道和MVPD共用分數*

## 帳戶共用機率 {#accounts-sharing-probability}

此圖表將共用機率的範圍從極低(0-20%)劃分為極高(80=100%)。

>[!NOTE]
>
>長條圖使用對數刻度。


![](assets/dashboard-ac-sharing-prob.png)


*圖：不同共用概率範圍中訂閱者帳戶的數量和百分比*

## 帳戶數和使用量（按共用機率級別） {#number-of-accounts-usage-sharing-probability}

此面板提供按共用概率的範圍劃分的帳戶的表格視圖，該範圍從極低(0-20%)到極高(80-100%)，每個五分之一的帳戶從共用帳戶的關聯使用量。

![](assets/no-acc-usage-prob-level.png)


*圖：在各種機率範圍中下降的帳戶、趨勢和使用數*

<!--
+++Dashboard for programmers

![dashboard of account IQ](assets/dashboard-capture.png)


*Figure: The dashboard*

>>>>>>> 7ab48cf61552febab21a5d5c05586e0aefe8ce17
## Average sharing score - aggregated for the current segment {#aggregated-sharing}

The Aggregated Sharing Score panel provides a top line readout summarizing the quantity and impact of sharing in terms of accounts and streaming volume.

The values help you understand the magnitude of credential sharing by your subscribers, hence providing a measure of the need to act upon it.

![](assets/aggregate-sharing-score.png)


*Figure: Average sharing score panel - aggregated for the current segment*

The following three metrics are components of the Average Sharing Score.

### Sharing level {#sharing-level}

The sharing level gauge shows the percentage of all your subscriber accounts (in the defined segment) that are shared, during the selected time frame.  

A value calculated based on an average of the sharing probability computed for every account for the selected MVPD(s) that has streamed from a one of the selected programmer channels during the selected time frame.

![](assets/sharing-level.png)


*Figure: Sharing level*

The Trend indicator shows the percentage change in the value of the metric in from the previous time frame.

### Usage from shared accounts {#usage-from-shared-accounts}

This gauge indicates what percent of the usage of all the subscriber accounts is from the shared accounts for the defined segment and time period. The gauge marks the ranges of usage (from shared accounts) on the scale of 0 to 100%. These ranges (named Low, Medium, High, and Abnormal) are based on the industry average.

You can also see the Trend indicator, which depicts a rise or fall in the usage from shared accounts as compared to the previous time frame.

![](assets/usage-4mshared-accounts.png)


*Figure: Usage from shared accounts*

### Overall sharing score {#overall-sharing-score}

Overall sharing score is composite of sharing scores including "Sharing level" and "Usage from shared accounts".

It provides a value meant to reflect the relative impact of sharing when compared to the industry. Its purpose is similar to that of a credit score, summarizing the situation with a single number. But in this case, the higher the number the greater the potential harm.

![](assets/overall-sharing-score.png)


*Figure: Overall sharing score*

## Industrywide overall sharing scores {#mvpd-in-segment}

+++Programmer- MVPDs in segment

This table provides a comparative view of the different Aggregated Sharing Scores for the MVPDs in the segment.

![](assets/mvpds-in-segment.png)


*Figure: Panel showing top MVPDs in a segment*


>[!NOTE]
>
>This table uses overall industry data for comparative purposes, not the data represented by those MVPDs in the segment.

+++

+++MVPD- Programmers in segment

This table provides a comparative view of the different Aggregated Sharing Scores for the programmers in the segment.

![](assets/programmers-in-segment.png)


*Figure: Panel showing top programmers in a segment*

+++


## Sharing score by channels and MVPDs {#sharin-score-by-channels-and-mvpds}

+++Programmer- MVPDs in segment

This table provides a comparative view of sharing scores of the selected channels for the MVPDs in the current segment.

![](assets/sharing-scores-by-channels-mvpds.png)


*Figure: Sharing scores by channels and MVPDs*

>[!NOTE]
>
>**Sharing score by channels and MVPDs** panel is available only for programmer login.

+++

## Accounts sharing probability distribution{#accounts-sharing-probab-dist}

This panel partitions accounts into ranges of sharing probability quintiles from very low (0-20%) to very high (80-100%).

Pie chart shows the proportions (in term of percentages) of user accounts in various sharing probability ranges. Whereas, column chart shows the absolute numbers of accounts in different probability ranges.

>[!NOTE]
>
>The column chart uses a logarithmic scale.


![](assets/dashboard-ac-sharing-prob.png)


*Figure: Percentages and number of subscriber accounts in different sharing probability ranges*

### Accounts over threshold in current segment {#acc-over-threshold-in-segment}

You can select a level of sharing probability, out of the following to view number and percentage of accounts above it:

* Over very low (0%-20%) probability

* Over low (20%-40%) probability

* Over moderate (40%-60%) probability

* Over high (60%-80%) probability

## Number of accounts and usage by sharing probability level {#number-of-accounts-usage-sharing-probability}

This panel provides tabular view of  accounts partitioned into ranges of sharing probability quintiles from very low (0-20%) to very high (80-100%) with each quintile's associated usage from shared accounts.

![](assets/no-acc-usage-prob-level.png)

*Figure: Number of accounts, trends, and usages falling in various probability ranges*

-->