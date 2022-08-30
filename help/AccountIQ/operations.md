---
title: 帳戶IQ中的操作
description: 帳戶IQ中的操作包括對訂閱者帳戶執行自動化和批量操作並跟蹤其效果。
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 5b34fbe26078ae761d61179975366505c5628c9c
workflow-type: tm+mt
source-wordcount: '0'
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

   報告以堆積柱形圖的形式顯示。

   ![](assets/operation-impact-report.png)

   *圖：操作報告，以查看操作的影響*

   X軸表示評估期間，Y軸表示操作的影響（以評估期間段中的帳戶數計算）。 每個桿被分成三部分。

   * 其中一部分表示仍滿足操作段標準的帳戶數。

   * 另一部分表示該期間的活動帳戶數，這些帳戶最初在該段中，但不再滿足該操作段的條件。

   * 第三部分是該期間未活動的帳戶。
   >[!NOTE]
   >
   >第一個欄表示在評估期間開始時滿足操作段條件的帳戶數。

   隨著時間的推移，該圖形通過指示與原始標準（例如，共用概率超過90且使用的設備超過5台）或已變為非活動的帳戶數，來顯示操作（通過操作）的效果。

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. 要關閉報告並返回主「操作」頁，請選擇 **操作** 選項 **操作** 的下界。

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->