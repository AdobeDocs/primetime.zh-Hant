---
title: 限制和已知問題
description: 產品中的已知問題。
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 已知問題和限制 {#known-issues}

Adobe致力於透過其產品提供強大的功能及順暢的使用者體驗。 Account IQ的目前版本（1.0版）以高度信賴度向串流提供者提供使用情況和訂閱共用分析。 不過，下列限制將在即將發行的版本中解決。

* 在儀表板或報告頁面中定義同類群組時，目前沒有新增量度的選項，例如 **裝置數量** 以調整區段。 此功能將在未來版本中提供。

* 在預估個別帳戶的分享分數時，帳戶IQ會採取保守的方法，讓公司能以高度信賴的方式進行共用。 但是，這種方法在彙總多個帳戶的總共用量時往往低估了總量。

* 此 [整體共用分數](/help/AccountIQ/dashboard.md#overall-sharing-score) 目前只有下列因素： [共用層級](/help/AccountIQ/dashboard.md#sharing-level) 和 [共用帳戶的使用情況](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). 未來版本會將其他量度納入考量。

* 在控制面板或報告頁面中定義同類群組時，MVPD和管道的選擇器目前缺乏搜尋機制。

* 在控制面板或報告頁面中定義同類群組時，限制僅可選取最多10個MVPD和程式設計師（或個別通道）。

* 截至目前，匯出帳戶統計資料的選項僅限於匯出1000個帳戶。

* 要選取的選項 [區段型別](#segment-type) 定義作業時，限製為 **固定帳戶數量**. 此 **帳戶數量可變** 選項將在即將推出的版本中提供。

* 目前左側導覽中的「基準」、「偵測模型」、「區段」、「快照」和「規則」區段已停用，並將在即將推出的版本中提供。

* 建立時 [作業](/help/AccountIQ/operation-affecting-user-segment.md)，您只能識別兩種 [動作](/help/AccountIQ/operation-affecting-user-segment.md) 至今為止 — 並行監視規則與外部動作。

* 目前，作業只能建立和 [已排程](/help/AccountIQ/operation-affecting-user-segment.md#action). 未來的版本可讓您暫停、繼續並完全管理這些專案。

* 由於使用的資料集較為有限，隔離模式無法真正反映共用的數量。 因此，隔離模式中的MVPD無法與任何其他MVPD做比較。 <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* 當您定義新的 [區段](/help/AccountIQ/segments-timeframe.md) 您可以為作業新增量度。 但如果您選取已儲存的區段，則無法新增更多量度來調整區段。

* 詳細程度和時間範圍選擇器限製為一週或一個月，這表示資料只能在一週或一個月內評估。

* 預先定義的間隔目前在詳細程度和時間範圍選擇器中是停用的，並將在未來的版本中提供。
