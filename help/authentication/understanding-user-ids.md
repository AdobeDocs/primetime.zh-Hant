---
title: 瞭解用戶ID
description: 瞭解用戶ID
exl-id: 813a8501-db72-4850-a387-c8db6120db80
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# 瞭解用戶ID {#understanding-user-ids}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

從概念上講，啟動權利流的每個用戶都與單個唯一的用戶ID相關聯。 但是，在權利流程的過程中，可以以不同的方式顯示一個用戶ID，這取決於您從哪個API獲取該ID。

的 `sessionGUID` 短媒體令牌是用戶ID的安全形式，可通過 `sendTrackingData()` 呼叫。 在所有當前整合中，這是跨時間和設備的用戶的持久GUID。 GUID的源以來自MVPD的驗證響應的用戶ID開頭。 但是，某些MVPD可能會在將來改變主意，並開始發送臨時GUID。 如果程式設計師希望確保AuthN響應中的MVPD源用戶ID是持久的，則他們應在與MVPD的協定中安排。

以下是用戶ID在Adobe Primetime驗證API中的不同表示方式：

| 屬性 | 目的 | 哈捨德 | 數字簽名 | 說明 |
| --- | --- | --- | --- | --- |
| sendTrackingData()GUID屬性 | 跟蹤/分析 | 是 | 否 | - MVPD用戶ID，由Adobe散列。 用戶ID無法追溯到源到MVPD。 </br> </br>  — 此形式的ID未進行數字簽名，因此對欺詐預防不安全。 但是，這對分析是足夠好的。  </br> </br>  — 在AuthN/AuthZ流中Adobe Primetime身份驗證生成的所有事件上都提供了此形式的用戶ID。 |
| 短媒體令牌的sessionGUID屬性 | 併發使用的欺詐跟蹤 | 是 | 是 |  — 這與通過sendTrackingData()的用戶ID相同，但是，此ID是數字簽名以保護其完整性，並且足夠用於欺詐跟蹤。 </br> </br>  — 使用我們的驗證程式庫後，將在伺服器端進行處理，並可在將視頻流發佈到客戶端之前分析欺詐模式。  任何這些任務都由程式設計師負責。 |
| getMetadata()userID屬性 | 帳戶連結，與MVPD的欺詐調查 | 否 | 否 |  — 此屬性允許Adobe向程式設計師公開實際源MVPD用戶ID。 </br> </br>  — 在Adobe的配置中，它可設定為加密或不加密（取決於MVPD首選項）。 如果加密，則使用提供給Adobe的程式設計師證書中的公鑰對其進行加密，以便客戶端不會清楚地暴露它。 </br> </br>  — 這為程式設計師提供了MVPD的實際用戶ID，因此它可以直接用於與MVPD的帳戶連結或欺詐調查。 |


**最後**

* 通常，MVPD提供持久唯一ID <u>並將其傳遞給Adobe成功驗證</u>。 它在所有網路中都是一致的。 例外是Comcast MVPD ，它為每個通道提供不同的用戶ID。

* MVPD用戶ID不包含PII，並且它不是帳號。 不需要以加密形式公開它，因為我們已通過所有未發送PII的MVPD驗證。

用戶ID的使用方式取決於用例：

* 如果您需要它進行跟蹤/分析，最實際的地方就是從 `sendTrackingData()`。
* 如果在伺服器端需要它來獲取流發佈、欺詐或操作資料，可以從媒體令牌驗證器獲取它。
* 如果您需要它來進行帳戶連結和更深入的欺詐活動，請與Adobe聯繫人聯繫以瞭解其可用性。
