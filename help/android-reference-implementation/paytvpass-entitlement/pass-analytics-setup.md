---
description: 您可以設定「參考實作」來使用Adobe Analytics報表。
title: 設定Adobe Analytics報表
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 設定Adobe Analytics報表 {#configure-adobe-analytics-reporting}

您可以設定「參考實作」來使用Adobe Analytics報表。

參考實作會設定為使用Primetime SDK內隨附的Adobe行動程式庫，將Primetime驗證事件資料傳送至Adobe Analytics。 若要啟用及使用從應用程式傳送的事件資料，您必須先建立Adobe Analytics帳戶。 建立帳戶之後：

1. 使用您的帳戶資訊設定應用程式；以及
1. 建立處理規則以自訂事件資料在報表中的顯示方式。

下表顯示傳送至Adobe Analytics的資料：

| 動作名稱 | `a.media.pass.event.MvpdSelection` | 使用者在選取對話方塊中選取了多頻道視訊程式設計散發者(MVPD) |
|---|---|---|
| 內容資料 | `a.media.pass.MvpdId (String)` | 使用者選取的MVPD |
|  | `a.media.pass.ClientType` | （字串）使用者端型別為「flash」、「html5」、「ios」或「android」 |
|  | | |
| 動作名稱 | `a.media.pass.event.AuthenticationDetection` | 驗證工作流程已完成 |
| 內容資料 | `a.media.pass.Successful` | （布林值） Token要求是否成功、true或false |
|  | `a.media.pass.MvpdId` | （字串）使用者選取的MVPD |
|  | `a.media.pass.Guid` | （字串）追蹤ID |
|  | `a.media.pass.Cached` | （布林值） Token已在快取中，true或false |
|  | `a.media.pass.ClientType` | （字串）使用者端型別為「flash」、「html5」、「ios」或「android」 |
|  | | |
| 動作名稱 | `a.media.pass.event.AuthorizationDetection` | 授權工作流程已完成 |
| 內容資料 | `a.media.pass.Successful` | （布林值） Token要求是否成功、true或false |
|  | `a.media.pass.MvpdId` | （字串）使用者選取的MVPD |
|  | `a.media.pass.Guid` | （字串）追蹤ID |
|  | `a.media.pass.Cached` | （布林值） Token已在快取中，true或false |
|  | `a.media.pass.Error` | （字串）授權嘗試失敗時的錯誤 |
|  | `a.media.pass.ErrorDetails` | （字串）其他錯誤詳細資料 |
|  | `a.media.pass.ClientType` | （字串）使用者端型別為「flash」、「html5」、「ios」或「android」 |

1. 設定應用程式以與Adobe Marketing Cloud搭配使用。

   若要啟用Primetime Primetime驗證資料傳送至Adobe Analytics，請執行以下作業： [!DNL `ADBMobileConfig.json`] 組態檔必須在編譯時新增到Reference實作。 請注意，此設定檔與Primetime SDK將視訊分析資料傳送至Marketing Cloud所使用的設定檔完全相同。 請參閱 [Adobe Marketing Cloud檔案](https://microsite.omniture.com/t2/help/en_US/reference/) 以取得有關使用Adobe Analytics帳戶設定應用程式的詳細資訊。
1. 建立處理規則。

   參考實作傳送的Primetime驗證事件資料不會自動出現在您的分析報表中。 您必須先透過建立處理規則來使用資料。 請參閱 [有關建立處理規則的Adobe Analytics檔案](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html).
