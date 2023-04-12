---
title: 了解使用者ID
description: 了解使用者ID
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# 了解使用者ID {#understanding-user-ids}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

從概念上講，起始權限流程的每個使用者都與單一、唯一的使用者ID相關聯。 不過，在權限流程中，根據您從哪個API取得ID，一個使用者ID可以以不同方式呈現。

此 `sessionGUID` 在短媒體代號中，代號是使用者ID的安全形式，可透過 `sendTrackingData()` 呼叫。 在所有目前的整合中，這是供使用者跨時間和裝置使用的永久GUID。 GUID的來源從來自MVPD的驗證回應的使用者ID開始。 不過，有些MVPD未來可能會改變心意，開始傳送暫時GUID。 如果程式設計師想要確保AuthN回應中的MVPD來源使用者ID是永久性的，他們應在與MVPD的合約中安排。

以下是Adobe Primetime驗證API中呈現使用者ID的不同方式：

| 屬性 | 用途 | 雜湊 | 數位簽署 | 說明 |
| --- | --- | --- | --- | --- |
| sendTrackingData()GUID屬性 | 追蹤/分析 | 是 | 否 | - MVPD使用者ID，依Adobe雜湊。 使用者ID無法追蹤回來源至MVPD。 </br> </br>  — 此形式的ID未進行數位簽名，因此不安全以防欺詐。 不過，這對分析來說已足夠好。  </br> </br>  — 在Adobe Primetime驗證在AuthN/AuthZ流程中產生的所有事件上，都會提供此使用者ID形式。 |
| 短媒體令牌的sessionGUID屬性 | 同時使用的欺詐追蹤 | 是 | 是 |  — 這與透過sendTrackingData()的使用者ID相同，不過，此ID是以數位簽署以保護其完整性，且足以用於欺詐追蹤。 </br> </br>  — 使用驗證器程式庫後，系統會在伺服器端處理它，且在將視訊資料流發佈至用戶端之前，可針對欺詐模式進行分析。  任何這些任務都由程式設計師負責。 |
| getMetadata()userID屬性 | 使用MVPD進行帳戶連結、欺詐調查 | 否 | 否 |  — 此屬性允許Adobe向程式設計師公開實際源MVPD用戶ID。 </br> </br>  — 在Adobe的設定中，可將其設為加密或不加密（視MVPD偏好設定而定）。 如果加密，則會用提供給Adobe的程式設計師證書中的公鑰加密，以便不會向客戶端明確公開。 </br> </br>  — 這為程式設計師提供了來自MVPD的實際用戶ID，因此，它可以直接與MVPD用於帳戶連結或欺詐調查。 |


**最後**

* 一般而言，MVPD會提供永久唯一ID <u>並在成功驗證時傳遞給Adobe</u>. 在所有網路中，它通常都是一致的。 Comcast MVPD是例外，它會為每個頻道提供不同的使用者ID。

* MVPD使用者ID不包含PII，也不是帳號。 由於我們已透過所有未傳送PII的MVPD驗證，因此不需要以加密的形式公開。

使用使用者ID的方式取決於使用案例：

* 如果您需要它來追蹤/分析，最實用的地方就是從 `sendTrackingData()`.
* 若您在伺服器端需要它來進行串流發行、詐騙或操作資料，可從Media Token驗證器取得。
* 如果您需要它來連結帳戶和進行更深層次的欺詐，請洽詢您的Adobe聯絡人以取得可用性。

