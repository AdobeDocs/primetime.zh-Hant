---
title: 對使用者區段建立操作並追蹤效果
description: 如何建立對定義的使用者區段產生影響並追蹤影響的操作。
exl-id: ab74f857-e178-4120-8f9c-655ec921d096
source-git-commit: dd1001d94e32a1a8b5346ff97b0f6cb7d244dcf2
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# 建立使用者區段的操作 {#operation-to-track-segment}

帳戶IQ的每個報表頁面都有 **建立新操作** 選項可協助您建立工作流程，以自動（並簡化）訂閱者帳戶上的各種（大量）動作；定義規則以指定範例、定義動作，以及記錄和分析這些動作的效果。 在要建立工序的頁上，您可以定義要對其執行工序的用戶組的抽樣，並計畫在將來日期運行該工序。

要建立操作，請執行以下操作：

1. 使用 [定義區段和時間範圍](/help/AccountIQ/howto-select-segment-timeframe.md).

1. 選擇 **建立新操作** 選項。 此 **建立新操作** 頁面。

   ![建立新操作的頁](assets/create-new-operations.png)
   *圖：要建立新操作的頁*

1. 在 **建立新操作** 填寫表單欄位中的詳細資訊，以了解：

   * [操作名稱](#operation-details) 操作詳細資訊
   * 在下運行操作的段 [目標區段](#segment) 並使用 [其他細分](#additional-segmentation)
   * [區段類型](#segment-type) 在 [目標區段](#segment)
   * [動作](#action)
   * [排程啟動](#schedule)

1. [保存操作](#save-operation).

## 操作詳細資訊 {#operation-details}

+++程式設計師 — 操作詳細資訊

將新操作命名為 **操作名稱** 「操作詳細資訊」下的欄位。 例如，「*測試多因素驗證對MVPD X訂閱者的影響」或「在並行監視中限制資料流數」或「限制MVPD D的訂閱者從20多台裝置檢視通道「N」*」。

+++

+++MVPD — 操作詳細資訊

將新操作命名為 **操作名稱** 「操作詳細資訊」下的欄位。 例如，「*測試多因素驗證對頻道N觀看者的影響」或「在並行監控中限制資料流的數量」或「限制來自20多台設備的訂閱者觀看頻道「N」*」。

+++

## 目標區段 {#segment}

+++程式設計師 — 目標段

此 **區段** 此處定義將由此操作操作的用戶；或操作的示例組。 預設區段為 **區段** 您選取的 [區段和時間範圍面板](/help/AccountIQ/howto-select-segment-timeframe.md) 在上述步驟1的主要報表或控制面板頁面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此區段會定義將受所建立操作影響的訂閱者。 例如，您選取的區段可能會指定 *MVPD的所有訂閱者帳戶（名為「C」，可檢視頻道「N運動」）*.

+++

+++MVPD — 目標區段

此 **區段** 此處定義將由此操作操作的用戶；或操作的示例組。 預設區段為 **區段** 您選取的 [區段和時間範圍面板](/help/AccountIQ/howto-select-segment-timeframe.md) 在上述步驟1的主要報表或控制面板頁面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此區段會定義將受所建立操作影響的訂閱者（特定頻道的檢視者）。 例如，您的（預設）區段包括 *觀看頻道「N運動」的所有訂閱者帳戶*.
+++

### 其他細分 {#additional-segmentation}

此外，您可以新增更多量度來調整目標區段。 例如，您可以新增大於90%的共用機率作為另一個量度。 現在，問題陳述 *&quot;為名為&#39;C&#39;的MVPD的訂閱者帳戶建立操作，這些帳戶正在觀看共用機率大於90%的頻道&#39;N Sports&#39;&quot;*.

![](assets/additional-segment.gif)

*圖：其他細分*

此外，如果通過添加設備數的其他度量來優化操作，則更新的問題陳述式將讀取 *&quot;為名為&#39;C&#39;的MVPD的訂閱者帳戶建立操作，這些帳戶正在觀看共用分數超過90且在評估期間使用超過5部裝置來檢視內容的頻道&#39;N Sports&#39;。&quot;*.

![](assets/refined-segment.png)

*圖：改善範例區段，包含整體共用分數和裝置數量量度*

如此一來，使用者群組就變得更精細。 因此，新增更多量度和條件後，您即可進一步讓區段定義要運作的帳戶。

### 區段類型 {#segment-type}

「段類型」是在整個工序評估期間處理段的方式。

![](assets/segment-type.png)

*圖：使用區段類型調整要運作的區段數*

<!--The segment type option allows you to further refine your segment based on the evaluation period (or time).

**Fixed number of accounts** 

When you select **Fixed number of accounts** segment type, then you need to specify an evaluation period as well.

By doing so, you are fixing the sample size for evaluation in terms of numbers. You are making Account IQ identify a specific set of users (that meet the criteria of defined evaluation period and segment metrics) to operate on. The analysis and graphs will be generated for this specific set of users only (identified initially) throughout the operation.

**Variable number of accounts**

When you select **Variable number of accounts** segment type, you do not limit the number of accounts in segment. The accounts which fall under the defined segment metrics are the part of the segment, and the number of accounts will change continuously during the course of operation.-->

>[!IMPORTANT]
>
>您只能使用 **固定帳戶數** 選項，從現在開始。 要選取的選項 **帳戶的變數** 即將發行的版本將提供。

<!--

you tell Account IQ in the beginning of the operation which number of accounts to operate on.

Account IQ system only has a segment definition, and during the operation it looks into all the accounts that fit that segments.

the number of accounts in segment is not limited, the accounts that fall under defined segment metrics will be part of the segment, and the no of accounts will change continuously, as there are no specific limitations - like an evaluation period in the past.When the segment is defined (which in this example is, subscriber accounts of MVPD 'C' who are viewing the channel 'N Sports' that have a sharing score above 80 and are using 10 different IPs) and we also identified a time period to evaluate a segment. This identifies X number of accounts as sample (for example 5000). How many devices they are using?
It identifies x-number of accounts (5000)...a very specific set of users that meet this criteria.
for every period that we schedule (within that operation) during that operation) we will look at those 5K users that are originally identified and we will present graph about them. How are the sharing scores coming up?u We identified a period. Are their sharing scores going up? Are there fewer of them who are meeting this definition?
Fixed versus variable is the way the treated in fixed or variable way.

1. we identified a fixed set of accounts.
2. we evaluate those specific accounts on criteria throughout the operation.

General idea independent of graph is that we will evaluate a set of accounts identified initially, for no of periods during operation and generate graphs against that.
Those are the 5000 users for which I will create graphs for for every period of the operation.

**Variable number of accounts**
We do not identify any initial set of accounts, we just have a segment definition.
Each period during the operation, we go and look into all the accounts that fit that segments.
If it is not a fixed segment, I won't initially evaluate it. I won't have an initial set of 5000. Instead at every period during the evaluation I will evaluate the segment then, and then I will produce graph about the next 3000 users.
the......will vary from period to period.

if not fixed segment, then I won't initially evaluate or have initial set of 5000, instead at every period during an operation and the.-->

## 動作 {#action}

此 **動作** 會定義您將對定義的區段執行的操作。

您可以採取兩種動作：

* 使用與帳戶IQ整合的系統的操作；例如 [併發監控](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)<!--, or Adobe Target-->.

* 建立及處理帳戶IQ外部且未與帳戶IQ系統整合之工作流程的動作。 例如，頻道程式設計員「N」向MVPD「C」的所有訂閱者發送大量電子郵件的動作。

>[!NOTE]
>
>通過建立操作，您不僅可以指定操作並定義其範圍，而且可以開始記錄這些操作的效果。

## 排程{#schedule}

您可以設定開始和結束日期，以排程操作的啟動。

>[!NOTE]
>
>使用定義區段時，開始日期和結束日期的粒度與您為評估選取的粒度相同 **區段和時間範圍面板**，在步驟1中。
>
>
>因此，如果您選取「周」作為粒度，則開始和結束日期會以周為單位（例如「周14」）;如果您選取「詳細程度」作為「月」，則開始和結束日期是以月為單位。


>[!IMPORTANT]
>
>開始日期必須晚於評估期，也必須晚於當前日期。 同樣地，結束日期也必須晚於開始日期和目前日期。

### 保存操作 {#save-operation}

儲存操作時，會顯示訊息畫面，通知您此操作中定義的區段也會儲存以供日後使用。 不過，您必須為此區段命名。

![](assets/save-operation.png)

*圖：儲存操作並指定區段名稱*

>[!NOTE]
>
>最佳實務是根據您要採取的動作，結合您要採取的區段來命名您的作業。

<!--In future you can select this saved segment when defining a segment for your analysis on the main reports page. Moreover, the saved segment is also listed when you create an operation the next time.

![](assets/saved-segment-operations-page.png)

*Figure: Saved segments in segment selector on Create new operations page* 

>[!IMPORTANT]
>
>When creating an operation, if you select a segment that was previously created then you cannot add new metrics to it and refine it.
>
>Adding new metrics creates a new segment, but you cannot modify an existing segment.-->

建立操作後，該操作將從開始日期運行到您指定的結束日期。

您可在主要 [操作](/help/AccountIQ/operations.md) 頁面。

![](assets/new-operation-created.png)

*圖：新建立的操作將列在主操作頁上*
