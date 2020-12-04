---
description: 您可以設定「參考實作」以使用Adobe Analytics報表。
seo-description: 您可以設定「參考實作」以使用Adobe Analytics報表。
seo-title: 設定Adobe Analytics報表
title: 設定Adobe Analytics報表
uuid: bdf8bb7f-a0c8-48a2-a632-0b872687f3fe
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 設定Adobe Analytics報表{#configure-adobe-analytics-reporting}

您可以設定「參考實作」以使用Adobe Analytics報表。

「參考實作」的設定是使用Primetime SDK內隨附的Adobe Mobile Library，將Primetime驗證事件資料傳送至Adobe Analytics。 若要啟用和使用從應用程式傳送的事件資料，您必須先建立Adobe Analytics帳戶。 帳戶建立後：

1. 使用您的帳戶資訊設定應用程式；和
1. 建立處理規則以自訂事件資料在報表中的顯示方式。

下表顯示傳送至Adobe Analytics的資料：

| 動作名稱 | `a.media.pass.event.MvpdSelection` | 使用者在選擇對話方塊中選取多頻道視訊程式設計裝置(MVPD) |
|---|---|---|
| 上下文資料 | `a.media.pass.MvpdId (String)` | 使用者選取的MVPD |
|  | `a.media.pass.ClientType` | （字串）用戶端類型為「flash」、「html5」、「ios」或「android」 |
|  |  |  |
| 動作名稱 | `a.media.pass.event.AuthenticationDetection` | 驗證工作流程已完成 |
| 上下文資料 | `a.media.pass.Successful` | （布林值）Token請求是成功、true或false |
|  | `a.media.pass.MvpdId` | （字串）使用者選取的MVPD |
|  | `a.media.pass.Guid` | （字串）追蹤ID |
|  | `a.media.pass.Cached` | （布林值）Token已在快取中，為true或false |
|  | `a.media.pass.ClientType` | （字串）用戶端類型為「flash」、「html5」、「ios」或「android」 |
|  |  |  |
| 動作名稱 | `a.media.pass.event.AuthorizationDetection` | 授權工作流程已完成 |
| 上下文資料 | `a.media.pass.Successful` | （布林值）Token請求是成功、true或false |
|  | `a.media.pass.MvpdId` | （字串）使用者選取的MVPD |
|  | `a.media.pass.Guid` | （字串）追蹤ID |
|  | `a.media.pass.Cached` | （布林值）Token已在快取中，為true或false |
|  | `a.media.pass.Error` | （字串）若授權嘗試失敗，則會發生錯誤 |
|  | `a.media.pass.ErrorDetails` | （字串）更多錯誤詳細資訊 |
|  | `a.media.pass.ClientType` | （字串）用戶端類型為「flash」、「html5」、「ios」或「android」 |

1. 設定應用程式以搭配Adobe Marketing Cloud使用。

   若要啟用將Primetime驗證資料傳送至Adobe Analytics，編譯時必須將[!DNL `ADBMobileConfig.json`]組態檔新增至「參考實作」。 請注意，這與Primetime SDK用來傳送視訊分析資料至Marketing Cloud的設定檔完全相同。 如需使用您的Adobe Analytics帳戶設定應用程式的詳細資訊，請參閱[Adobe Marketing Cloud檔案](https://microsite.omniture.com/t2/help/en_US/reference/)。
1. 建立處理規則。

   「參考實作」所傳送的Primetime驗證事件資料不會自動出現在您的分析報表中。 您必須先建立處理規則，以利用資料。 請參閱[Adobe Analytics檔案，瞭解如何建立處理規則](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html)。
