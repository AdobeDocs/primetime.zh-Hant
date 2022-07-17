---
title: 限制和已知問題
description: '產品中的已知問題。 '
source-git-commit: 4b840a1a722b3dd403d70f4ba838529d7d4d0b35
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# 已知問題和限制 {#known-issues}

Adobe致力於通過其產品提供強大的功能和無縫的用戶體驗。 Account IQ的當前版本（版本1.0）為流式處理提供程式提供了高度信任的使用和訂閱共用分析。 但是，在即將發佈的版本中將解決以下限制。

* 在儀表板或報表頁中定義組時，當前沒有添加度量的選項，如 **設備數** 以細化段。 此功能將在未來版本中提供。

* 在估算個人賬戶的分數時，Account IQ採取了一種保守的方法，使公司能夠以高度的自信來採取行動分享。 但是，這種方法往往低估了在多個帳戶之間合計時的共用總量。

* 的 [總體共用分數](/help/AccountIQ/dashboard.md#overall-sharing-score) 當前僅有因素 [共用級別](/help/AccountIQ/dashboard.md#sharing-level) 和 [來自共用帳戶的使用情況](/help/AccountIQ/dashboard.md#usage-from-shared-accounts)。 未來版本將考慮其他指標。

* 在儀表板或報表頁中定義組時，MVPD和通道的選擇器目前缺少搜索機制。

* 在儀表板或報表頁中定義組時，最多只能選擇10個MVPD和程式設計師。

* 截至目前，導出帳戶統計資訊的選項僅限於導出1000個帳戶。

* 要選擇的選項 [段類型](#segment-type) 當定義操作時 **固定帳戶數**。 的 **帳戶的變數數** 選項。

* 左導航中的Benchmarking 、 Detection Models 、 Segments 、 Snapshots和Rules部分當前已禁用，並將在即將發佈的版本中提供。

* 建立時 [操作](/help/AccountIQ/operation-affecting-user-segment.md)你只能識別兩種 [操作](/help/AccountIQ/operation-affecting-user-segment.md) 截至目前 — 併發監視規則和外部操作。

* 當前，只能建立和 [計畫](/help/AccountIQ/operation-affecting-user-segment.md#action)。 將來的版本將允許您暫停、恢復和完全管理它們。

* 由於使用的資料集較為有限，隔離模式沒有真正反映共用量。 因此，無法將隔離模式下的MVPD與任何其他MVPD進行比較。

* 定義新 [分部](/help/AccountIQ/segments-timeframe.md) 對於可添加度量的操作。 但是，如果選擇已保存的段，則無法添加更多度量來細化段。

* 粒度和時間框架選擇器限於一週或一個月，這意味著資料只能在一週或一個月內進行評估。

* 預定義的時間間隔當前在粒度和時間範圍選擇器中被禁用，將來版本中將提供。
