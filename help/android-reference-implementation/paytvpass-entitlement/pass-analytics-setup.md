---
description: 您可以設定「參考實施」以使用Adobe Analytics報告。
title: 配置Adobe Analytics報告
exl-id: 3607f9d4-1069-4722-af0b-121223125112
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 配置Adobe Analytics報告 {#configure-adobe-analytics-reporting}

您可以設定「參考實施」以使用Adobe Analytics報告。

參考實現被配置為使用在黃金時段SDK中捆綁的Adobe移動庫向Adobe Analytics發送黃金時段驗證事件資料。 要啟用和使用從應用程式發送的事件資料，必須首先建立一個Adobe Analytics帳戶。 建立帳戶後：

1. 使用帳戶資訊配置應用程式；和
1. 建立處理規則以自定義事件資料在報告中的顯示方式。

下表列出了發往Adobe Analytics的資料：

| 操作名稱 | `a.media.pass.event.MvpdSelection` | 用戶在選擇對話框中選擇了多通道視頻節目分配器(MVPD) |
|---|---|---|
| 上下文資料 | `a.media.pass.MvpdId (String)` | 用戶選擇的MVPD |
|  | `a.media.pass.ClientType` | （字串）客戶端類型為&quot;flash&quot;、&quot;html5&quot;、&quot;ios&quot;或&quot;android&quot; |
|  |  |  |
| 操作名稱 | `a.media.pass.event.AuthenticationDetection` | 驗證工作流已完成 |
| 上下文資料 | `a.media.pass.Successful` | （布爾型）令牌請求是成功、true還是false |
|  | `a.media.pass.MvpdId` | （字串）用戶選擇的MVPD |
|  | `a.media.pass.Guid` | （字串）跟蹤ID |
|  | `a.media.pass.Cached` | （布爾值）快取中已有的令牌，True或False |
|  | `a.media.pass.ClientType` | （字串）客戶端類型為&quot;flash&quot;、&quot;html5&quot;、&quot;ios&quot;或&quot;android&quot; |
|  |  |  |
| 操作名稱 | `a.media.pass.event.AuthorizationDetection` | 授權工作流已完成 |
| 上下文資料 | `a.media.pass.Successful` | （布爾型）令牌請求是成功、true還是false |
|  | `a.media.pass.MvpdId` | （字串）用戶選擇的MVPD |
|  | `a.media.pass.Guid` | （字串）跟蹤ID |
|  | `a.media.pass.Cached` | （布爾值）快取中已有的令牌，True或False |
|  | `a.media.pass.Error` | （字串）授權嘗試失敗時出錯 |
|  | `a.media.pass.ErrorDetails` | （字串）更多錯誤詳細資訊 |
|  | `a.media.pass.ClientType` | （字串）客戶端類型為&quot;flash&quot;、&quot;html5&quot;、&quot;ios&quot;或&quot;android&quot; |

1. 配置應用程式以與Adobe Marketing Cloud一起使用。

   啟用黃金時段驗證資料發送至Adobe Analytics, [!DNL `ADBMobileConfig.json`] 必須在編譯時將配置檔案添加到「引用實現」中。 請注意，這與Mognishe SDK用於將視頻分析資料發送到Marketing Cloud的配置檔案完全相同。 請咨詢 [Adobe Marketing Cloud文檔](https://microsite.omniture.com/t2/help/en_US/reference/) 的子菜單。
1. 建立處理規則。

   參考實施發送的黃金時段身份驗證事件資料不會自動顯示在分析報告中。 必須先通過建立處理規則來利用資料。 請咨詢 [Adobe Analytics關於建立處理規則的文檔](https://microsite.omniture.com/t2/help/en_US/reference/processing_rules.html)。
