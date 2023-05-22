---
title: 對用戶段和跟蹤效果建立操作
description: 如何建立操作，以影響和跟蹤對已定義用戶段的影響。
exl-id: ab74f857-e178-4120-8f9c-655ec921d096
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 在用戶段上建立操作 {#operation-to-track-segment}

帳戶IQ上的每個報告頁都有 **建立新操作** 選項，幫助您建立工作流以自動化（並簡化）訂戶帳戶上的各種（批量）操作；定義規則以指定示例、定義操作以及記錄和分析這些操作的效果。 在要建立操作的頁上，您可以定義要在其上執行操作的用戶組示例，並將操作安排在將來日期運行。

要建立操作：

1. 使用中的步驟定義段（組）以分析任何報表或儀表板頁 [定義段和時間範圍](/help/AccountIQ/howto-select-segment-timeframe.md)。

1. 選擇 **建立新操作** 選項。 的 **建立新操作** 的上界。

   ![建立新操作的頁](assets/create-new-operations.png)
   *圖：要建立新操作的頁*

1. 在 **建立新操作** 的子菜單。

   * [操作名稱](#operation-details) 在操作詳細資訊中
   * 要在下運行操作的段 [目標段](#segment) 並使用 [附加分段](#additional-segmentation)
   * [段類型](#segment-type) 在 [目標段](#segment)
   * [操作](#action)
   * [計畫激活](#schedule)

1. [保存操作](#save-operation)。

## 操作詳細資訊 {#operation-details}

+++程式設計師操作詳細資訊

將新操作命名為 **操作名稱** 欄位。 例如， &quot;*Test多重身份驗證對MVPD X訂戶的影響」或「限制併發監視中的流數」或「限制MVPD D訂戶查看20多台設備的通道「N」*。

+++

+++MVPD — 操作詳細資訊

將新操作命名為 **操作名稱** 欄位。 例如， &quot;*Test多因素身份驗證對頻道N查看器的影響」或「限制併發監視中的流數」或「限制訂閱者從20多台設備查看頻道「N」*。

+++

## 目標段 {#segment}

+++程式設計師 — 目標段

的 **段** 這裡定義了將由此操作操作的用戶；或操作的示例組。 預設段為 **分部** 已使用 [段和時間面板](/help/AccountIQ/howto-select-segment-timeframe.md) 在上面步驟1的主報表或儀表板頁面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此段定義將受所建立操作影響的訂戶。 例如，所選段可能會指定 *查看頻道「N Sports」的名為「C」的MVPD的所有訂閱者帳戶*。

+++

+++MVPD — 目標段

的 **段** 這裡定義了將由此操作操作的用戶；或操作的示例組。 預設段為 **分部** 已使用 [段和時間面板](/help/AccountIQ/howto-select-segment-timeframe.md) 在上面步驟1的主報表或儀表板頁面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此段定義將受所建立操作影響的訂閱者（特定渠道的查看者）。 例如，您的（預設）段包括 *查看頻道「N Sports」的所有訂閱者帳戶*。
+++

### 附加分段 {#additional-segmentation}

此外，您還可以通過添加更多度量來細化目標段。 例如，可以添加大於90%的共用概率作為另一個度量。 現在問題陳述里 *&quot;為名為&quot;C&quot;的MVPD的訂戶帳戶建立操作，這些帳戶正在查看共用概率大於90%的頻道&quot;N Sports&quot;&quot;*。

![](assets/additional-segment.gif)

*圖：附加分段*

此外，如果通過添加設備數的另一個度量來細化操作，則更新的問題語句將讀取 *&quot;為名為&quot;C&quot;的MVPD的訂戶帳戶建立操作，這些帳戶正在查看共用分數超過90且在評估期間使用5台以上設備查看內容的頻道&quot;N Sports&quot;。&quot;*。

![](assets/refined-segment.png)

*圖：具有總體共用分數和設備數量度量的精細示例段*

通過這樣，用戶組變得更精細。 因此，通過添加更多的指標和條件，您將進一步限定該段以定義要操作的帳戶。

### 段類型 {#segment-type}

段類型是在整個工序評估期間處理段的方式。

![](assets/segment-type.png)

*圖：使用段類型細化要操作的段數*

<!--The segment type option allows you to further refine your segment based on the evaluation period (or time).

**Fixed number of accounts** 

When you select **Fixed number of accounts** segment type, then you need to specify an evaluation period as well.

By doing so, you are fixing the sample size for evaluation in terms of numbers. You are making Account IQ identify a specific set of users (that meet the criteria of defined evaluation period and segment metrics) to operate on. The analysis and graphs will be generated for this specific set of users only (identified initially) throughout the operation.

**Variable number of accounts**

When you select **Variable number of accounts** segment type, you do not limit the number of accounts in segment. The accounts which fall under the defined segment metrics are the part of the segment, and the number of accounts will change continuously during the course of operation.-->

>[!IMPORTANT]
>
>您只能使用 **固定帳戶數** 選項。 要選擇的選項 **帳戶的變數數** 將在即將發佈的版本中提供。

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

## 操作 {#action}

的 **操作** 定義要對定義的段執行的操作。

可以執行兩種操作：

* 使用與Account IQ整合的系統的操作；例如 **併發監視** <!--[Concurrency Monitoring](https://tve.helpdocsonline.com/concurrency-monitoring-introduction), or Adobe Target-->。

* 建立和處理帳戶IQ外部且未與帳戶IQ系統整合的工作流的操作。 例如，渠道程式設計師「N」向MVPD「C」的所有訂閱者發送批量電子郵件的操作。

>[!NOTE]
>
>通過建立操作，您不僅可以指定操作並定義其範圍，還可以開始記錄這些操作的效果。

## 計畫{#schedule}

您可以通過設定起始日期和終止日期來安排操作的激活。

>[!NOTE]
>
>開始日期和結束日期的粒度與定義段時為評估選擇的粒度相同 **段和時間面板**&#x200B;的子菜單。
>
>
>因此，如果您選擇粒度為「周」，則開始日期和結束日期將以周為單位（例如，「周14」）;如果選擇粒度為「月」，則起始日期和終止日期以月為單位。


>[!IMPORTANT]
>
>開始日期必須晚於評估期間，也遲於當前日期。 同樣，結束日期也必須晚於開始日期和當前日期。

### 保存操作 {#save-operation}

保存操作時，將顯示一個消息螢幕，通知您此操作中定義的段也將保存到將來。 但是，您需要命名此段。

![](assets/save-operation.png)

*圖：保存操作並指定段名稱*

>[!NOTE]
>
>根據您所採取的行動與您將要執行的活動段相結合，為您的操作命名是一種最佳做法。

<!--In future you can select this saved segment when defining a segment for your analysis on the main reports page. Moreover, the saved segment is also listed when you create an operation the next time.

![](assets/saved-segment-operations-page.png)

*Figure: Saved segments in segment selector on Create new operations page* 

>[!IMPORTANT]
>
>When creating an operation, if you select a segment that was previously created then you cannot add new metrics to it and refine it.
>
>Adding new metrics creates a new segment, but you cannot modify an existing segment.-->

建立操作後，該操作將從開始日期運行到您指定的結束日期。

在首頁上可以查看已保存操作的詳細資訊 [操作](/help/AccountIQ/operations.md) 的子菜單。

![](assets/new-operation-created.png)

*圖：新建立的操作將在主「操作」頁上列出*
