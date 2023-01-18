---
title: 導出共用分數高的帳戶的資訊
description: 導出共用分數高的帳戶的資訊。
exl-id: df41ddd2-fde3-4861-abd4-6e32f0be9ea5
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# 導出共用分數高的帳戶的資訊 {#export-account-info-high-score}

帳戶IQ可讓您選擇根據前1000個訂閱者帳戶的帳戶共用詳細資訊匯出 [共用機率](/help/AccountIQ/product-concepts.md#account-sharing-probability-def). 匯出的CSV檔案中的資料會依照 [區段](/help/AccountIQ/product-concepts.md#segment-def)，針對 [指定時間範圍](/help/AccountIQ/product-concepts.md#time-frame-def).

匯出帳戶共用資訊的選項可在 [一般使用情況報表](/help/AccountIQ/general-usage-reports.md) 和 [共用帳戶報表](/help/AccountIQ/shared-acc-reports.md) 頁面。

>[!NOTE]
>
>「一般使用情形」和「共用帳戶」報表頁面所下載的CSV檔案中的數字不同。 這是因為「一般使用情況報表」頁面有其他篩選器，供程式設計師為裝置、IP和郵遞區號的數量選取臨界值。 因此，從「一般使用情況」報表匯出的資料是以套用的其他臨界值篩選為基礎。

![導出選項（一般用法）](assets/export.png)

要導出訂閱者的帳戶共用資訊，請執行以下操作：

1. 依照 [如何定義區段和選取時間範圍](/help/AccountIQ/howto-select-segment-timeframe.md) 從 [區段與時間範圍](/help/AccountIQ/segments-timeframe.md) 中。

1. 選取 **導出前1000個帳戶** 為1000個訂閱者匯出帳戶資訊的選項，共用機率最高。

使用導出選項時，將將共用概率最高的1000個帳戶的統計資訊（定義的時間範圍）下載到本地電腦的「下載」資料夾中。

>[!NOTE]
>
>下載的CSV檔案可使用任何讀取CSV檔案的應用程式來開啟，例如Microsoft Excel。

![以csv格式匯出資料](assets/exported-csv.png)

*圖：匯出的共用帳戶資料為CSV格式*

## 匯出報表中的欄 {#columns-in-export}

**周/月**

您在 **粒度和時間範圍** 區段選取器中的「 」選項，以尋找共用統計資料。

**MVPD**

如果您是程式設計師使用者，欄會顯示訂閱者帳戶所屬的MVPD。

**訂閱者Id**

我們連續討論的特定帳戶。

**最少設備數**

實際裝置數量（該資料流內容）幾乎肯定大於為特定帳戶指定的最小裝置數量。

>[!NOTE]
>
>實際裝置數量（該資料流內容）肯定大於為特定帳戶指定的最小裝置數量。

**最低人數**

使用這些裝置進行活動串流內容的絕對最小人數。

>[!NOTE]
>
>實際人數（該流內容）幾乎肯定比為特定賬戶指定的最低人數大得多。

**IP數**

內容流的IP地址數。

**#位置**

內容串流所在的位置數（根據郵遞區號）。

**#城市**

流播的城市數。

**狀態數**

進行串流的州數。

**#群集**

相異數 [叢集](/help/AccountIQ/product-concepts.md#cluster-def) 流媒體流。

**地理範圍（英里）**

與帳戶相關聯的串流位置之間的最大距離。

**# AuthN確定**

使用者在此期間使用該帳戶登入的次數。

**#驗證Z確定**

MVPD已授權資料流或授予該帳戶存取權（內容）的次數。

**播放請求數**

時段內的實際資料流數。

>[!NOTE]
>
>**#驗證Z確定** 通常小於 **播放請求數** 因為Adobe會快取來自MVPD的授權長達24小時。 此欄不適用於MVPD。

**通道數**

帳戶在該時段內已觀看的不同管道總數。

>[!NOTE]
>
>**通道數** 包括不一定屬於登錄程式設計師的通道。
>
>帳戶的此數字之所以顯示，是因為帳戶已觀看您的管道，但在該時段內也存取其他管道。

**使用模式**

此欄中的數字是識別碼，會對應至我們將所有使用者帳戶識別為的14種模式之一。

*表：匯出的CSV對應與使用模式中的使用模式識別碼*

| ID | 1 | 2 | 3 | 4 | 5和8 | 6 | 7 | 9 | 10和11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 使用模式 | 一般使用者 | 旅行者或通勤者 | 大家庭 | 親朋好友 | 社交群組共用 | 一大群朋友 | 同時串流 | 社群分享 | 不確定行為 | 小家庭 | 第二個家 | 使用異常 |

{style=&quot;table-layout:auto&quot;}

**共用機率**

共用機率是特定帳戶共用其認證的機率。

>[!NOTE]
>
> 所有帳戶的共用機率（在選取的區段中）平均用於計算 [共用級別](/help/AccountIQ/dashboard.md#sharing-level) 的 [匯總分享分數](/help/AccountIQ/dashboard.md#aggregated-sharing).
