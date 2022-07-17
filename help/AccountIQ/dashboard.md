---
title: 帳戶IQ儀表板
description: '儀表板通過分析大量訂閱者資料幫助查明密碼共用實例。  '
source-git-commit: f6f1769d86a98d3a545bf986e41e9ba2252a36ff
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# 儀表板 {#dashboard}

「控制面板」匯總和聚合圖表和報表的集合中的資料，這些圖表和報表旨在對帳戶共用的範圍和影響進行高級別概述。 它提供一頁，其中包含來自帳戶IQ的主要報告和度量。

![帳戶IQ儀表板](assets/dashboard-capture.png)

## 聚合共用分數 {#aggregated-sharing}

「聚合共用分數」面板提供頂行讀出，概括了從帳戶和流量量角度共用的數量和影響。

這些值有助於您瞭解訂閱者共用憑據的大小，從而提供了對此採取行動的必要性的度量。

![](assets/aggregate-sharing-score.png)

以下三個指標是聚合共用分數的元件。

### 共用級別 {#sharing-level}

共用級別規格顯示在所選時間範圍內共用的所有訂閱伺服器帳戶（在定義的段中）的百分比。

基於在所選時間幀期間從所選程式設計師通道之一流化的一組所選MVPD中的每個帳戶計算的共用概率的平均值計算的值。

![](assets/sharing-level.png)

趨勢指示器顯示度量值與上一時間幀相比的百分比變化。

### 來自共用帳戶的使用 {#usage-from-shared-accounts}

此標尺指示所有訂閱者帳戶的使用百分比來自定義的段和時間段的共用帳戶。 該儀表將使用範圍（從共用帳戶）標籤為0到100%。 這些範圍（稱為「低」、「中」、「高」和「異常」）均基於行業平均值。

您還可以看到「趨勢」指示器，它描述了與上一個時間框架相比來自共用帳戶的使用情況的增減。

![](assets/usage-4mshared-accounts.png)

### 總體共用分數 {#overall-sharing-score}

總體共用分數是共用分數的組合，包括「共用級別」和「共用帳戶的z使用」。

它提供的價值旨在反映與行業相比共用的相對影響。 目的類似於信用評分，用一個數字來概括情況。 但在這種情況下，數量越大，潛在的傷害就越大。

![](assets/overall-sharing-score.png)

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)-->

### 全行業MVPD總體共用分數 {#top-mvpds}

此表提供了段中MVPD的不同聚合共用分數的比較視圖。

>[!NOTE]
>
>此表使用整個行業資料進行比較，而不是段中那些MVPD所表示的資料。

![](assets/top-mvpds.png)

### 按渠道和MVPD共用分數 {#sharin-score-by-channels-and-mvpds}

此表提供了共用當前段中MVPD的選定通道分數的比較視圖。

![](assets/sharing-scores-by-channels-mvpds.png)

### 帳戶共用概率 {#accounts-sharing-probability}

此圖表將共用概率的範圍從非常低(0-20%)劃分為非常高(80=100%)。

>[!NOTE]
>
>條形圖使用對數刻度。


![](assets/dashboard-ac-sharing-prob.png)

### 通過共用概率級別計算的帳戶數和使用情況 {#number-of-accounts-usage-sharing-probability}

此面板提供了帳戶的表格視圖，這些帳戶被劃分為從非常低(0-20%)到非常高(80=100%)的共用概率，每個五分之一的帳戶從共用帳戶的相關使用量。

![](assets/no-acc-usage-prob-level.png)
