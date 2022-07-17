---
title: 帳戶IQ中的操作
description: 帳戶IQ中的操作包括對訂閱者帳戶執行自動化和批量操作並跟蹤其效果。
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# 操作 {#operations-tab-next-steps}

一旦您瞭解了訂閱者的使用模式並識別了選定段的密碼共用（使用帳戶智商中的報告和分析），您就可以針對目標採取有針對性的措施來減少密碼共用。

帳戶IQ中的操作功能可幫助您通過稱為操作的重點過程有效地處理和管理憑據共用。 它為您提供了為特定訂閱者帳戶組設計目標、根據目標定制目標操作以及在將來一段時間內自動執行這些操作的選項。 通過「操作」功能，您不僅可以建立和執行操作，還可以評估操作的影響。 因此，通過評估影響，您可以調整策略以優化效果，無論是轉換借款人還是減少憑據共用。

查看 **操作** 頁面選擇 **操作** 選項 **操作** 在帳戶IQ應用程式的左側導航中。 「操作」頁列出了帳戶IQ系統上已存在的所有操作及其詳細資訊。

![](assets/operations-page.png)

*圖：帳戶IQ中現有操作的清單和詳細資訊*

在「操作」頁上，您可以：

* 查看帳戶IQ中已存在的操作清單

* 查看操作詳細資訊，如：

   * 狀態（已調度、正在運行、已結束、錯誤或已停止）

   * 進度（完成百分比）

   * 目標受眾（運行操作的段）

   * 計畫（操作開始和結束日期）

   * 操作的建立和結束日期

* [建立新操作](/help/AccountIQ/operation-affecting-user-segment.md)

* [查看操作報表](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## 查看操作報表 {#operation-reports}

您可以通過查看操作的報告來分析其影響。 要查看工序的報表，請執行以下操作：

1. 在「操作」首頁上選擇操作名稱。

   報告以堆疊條形圖的形式顯示。

   ![](assets/operation-impact-report.png)

   *圖：操作報告，以查看操作的影響*

   x軸繪製評估週期，y軸繪製變數以測量操作的影響。

   例如，在上圖中，y軸上的變數是帳戶數。 查看此圖表時，您可以比較操作段中的帳戶數與特定時間（如操作評估期的第2週）操作段外的帳戶數。 因此，您可以分析評估期間內操作段內和段外帳戶數的變化情況。

   因此，如果您的操作是向懷疑的帳戶發送警告電子郵件，而操作段中的帳戶共用概率超過90且使用5個以上設備來流內容，則在評估期開始時，該段中的帳戶超過700萬。 該數字在圖表所示的評估期間發生變化，從而指示操作的影響。 根據評估，您可以對疑似帳戶採取補救措施，或繼續操作，或調整策略以獲得更好的結果以限制憑據共用。

2. 要關閉報告並返回主「操作」頁，請選擇 **操作** 選項 **操作** 的下界。

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->