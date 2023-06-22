---
title: 帳戶IQ中的作業
description: 帳戶IQ中的作業涉及對訂閱者帳戶執行自動化和大量作業並追蹤其影響的動作。
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 5b34fbe26078ae761d61179975366505c5628c9c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 作業 {#operations-tab-next-steps}

瞭解訂閱者的使用模式，並為選取的區段找出密碼共用（使用Account IQ中的Reports &amp; Analytics）後，您就可以針對目標採取鎖定行動，減少密碼共用的情形。

帳戶IQ中的作業功能可透過稱為作業的重點程式，協助您有效處理及管理憑證共用。 它提供您為特定訂閱者帳號群組設計目標、量身打造目標動作（根據目標），以及在未來期間自動執行這些動作的選項。 透過「作業」功能，您不僅可以建立和執行作業，而且可以評估其影響。 因此，透過評估影響，您可以調整策略以最佳化影響，無論是轉換借款人還是緩解憑證共用。

檢視 **作業** 頁面選取 **作業** 下的選項 **動作** 帳戶IQ應用程式的左側導覽中。 「作業」頁面會列出「帳戶IQ」系統上現有的所有作業及其詳細資訊。

![](assets/operations-page.png)

*圖：帳戶IQ中現有作業的清單和詳細資訊*

您可以在「作業」頁面執行下列作業：

* 檢視帳戶IQ中已存在的作業清單

* 檢視作業詳細資料，例如：

   * 狀態（已排程、執行中、已結束、錯誤或已停止）

   * 進度（完成百分比）

   * 目標對象（執行操作的區段）

   * 排程（作業的開始與結束日期）

   * 作業的建立與結束日期

* [建立新作業](/help/AccountIQ/operation-affecting-user-segment.md)

* [檢視作業報告](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## 檢視作業報告 {#operation-reports}

您可以檢視作業的報告，分析作業的影響。 若要檢視作業報表，請執行下列步驟：

1. 在主「作業」頁面上選取作業名稱。

   報表會以棧疊欄圖表的形式顯示。

   ![](assets/operation-impact-report.png)

   *圖：作業報告，用於檢視作業的影響*

   X軸代表評估期間，而Y軸則描述作業的影響（以評估期間節段中的科目數目表示）。 每個長條都會分成三個部分。

   * 一部分代表仍符合作業節段條件的科目數目。

   * 另一個部分代表該期間的有效科目數目，這些科目最初位於區段中，但不再符合作業區段的條件。

   * 第三部分代表該期間未啟用的帳戶。
   >[!NOTE]
   >
   >第一列代表評估期間開始時，符合作業節段條件的科目數目。

   在一段時間內，圖表會透過指示帳戶數目來顯示您動作（透過作業）的效果，這些帳戶相對於原始條件已變更其行為（例如，共用機率超過90且使用5部以上的裝置），或已變為非作用中。

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. 若要關閉報表並返回主要「作業」頁面，請選取「 」 **作業** 下的選項 **動作** 在左側導覽中。

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->