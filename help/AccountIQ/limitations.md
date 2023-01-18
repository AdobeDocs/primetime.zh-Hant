---
title: 限制和已知問題
description: 產品中的已知問題。
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 已知問題和限制 {#known-issues}

Adobe致力於透過其產品提供強大的功能和順暢的使用者體驗。 目前版本（1.1版）的帳戶IQ，能為串流提供者提供高度信賴的使用與訂閱共用分析。 不過，未來版本將解決下列限制。

* 在控制面板或報表頁面中定義同類群組時，目前沒有可新增度量的選項，例如 **設備數** 來調整區段。 此功能將於近期推出。

* 在預估個別帳戶的共用分數時，帳戶IQ會採取保守的方法，讓公司能有極大的信賴來採取共用行動。 但是，此方法往往會低估在多個帳戶中匯總時的共用總量。

* 此 [整體共用分數](/help/AccountIQ/dashboard.md#overall-sharing-score) 目前僅限 [共用層級](/help/AccountIQ/dashboard.md#sharing-level) 和 [來自共用帳戶的使用情況](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). 未來版本會納入其他量度。

* 在控制面板或報表頁面中定義同類群組時，MVPD和管道的選取器目前缺乏搜尋機制。

* 在控制面板或報表頁面中定義同類群組時，僅限選取最多10個MVPD和程式設計人員（或個別頻道）。

* 截至目前，匯出帳戶統計資料的選項僅限於匯出1000個帳戶。

* 要選取的選項 [區段類型](#segment-type) 定義操作時限於 **固定帳戶數**. 此 **帳戶的變數** 選項將在即將發行的版本中提供。

* 左側導覽中的基準、偵測模型、區段、快照和規則區段目前已停用，且將在即將推出的版本中使用。

* 建立 [作業](/help/AccountIQ/operation-affecting-user-segment.md)，您只能識別兩種 [動作](/help/AccountIQ/operation-affecting-user-segment.md) 截至目前 — 並行監視規則和外部操作。

* 目前，只能建立和 [排程](/help/AccountIQ/operation-affecting-user-segment.md#action). 未來版本可讓您暫停、繼續並完全管理這些版本。

* 由於所使用的資料集較有限，隔離模式無法真正反映共用的量。 因此，隔離模式下的MVPD無法與任何其他MVPD進行比較。 <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* 定義新 [區段](/help/AccountIQ/segments-timeframe.md) 您可以為操作新增量度。 但如果您選取儲存的區段，則無法新增更多量度來調整區段。

* 粒度和時間範圍選取器限制為一週或一個月，這表示只能在一週或一個月評估資料。

* 預先定義的間隔目前在粒度和時間範圍選擇器中是停用的，未來版本將可供使用。
