---
title: 瞭解使用者ID
description: 瞭解使用者ID
exl-id: 813a8501-db72-4850-a387-c8db6120db80
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# 瞭解使用者ID {#understanding-user-ids}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

在概念上，每個起始權利流程的使用者都與單一不重複的使用者ID相關聯。 不過，在軟體權利檔案流程的過程中，該使用者ID可能會以不同的方式呈現，具體取決於您從哪個API取得該ID。

此 `sessionGUID` 短媒體Token中的是使用者ID的安全形式，可透過 `sendTrackingData()` 呼叫。 在目前的所有整合中，這是使用者在不同時間和裝置上的永久GUID。 GUID的來源以來自MVPD之驗證回應的使用者ID開頭。 不過，有些MVPD未來可能會改變心意，並開始傳送暫時GUID。 如果程式設計師想要確保AuthN回應中的MVPD來源使用者ID是永久性的，他們應在與MVPD的合約中安排此ID。

以下是Adobe Primetime驗證API中表示使用者ID的不同方式：

| 屬性 | 用途 | 雜湊 | 數位簽署 | 說明 |
| --- | --- | --- | --- | --- |
| sendTrackingData() GUID屬性 | 追蹤/分析 | 是 | 否 | - MVPD使用者ID，以Adobe雜湊處理。 使用者ID無法回溯至MVPD的來源。 </br> </br>  — 此形式的ID未經數位簽署，因此對於防止欺詐而言並不安全。 不過，這已足夠Analytics。  </br> </br>  — 在Adobe Primetime驗證於AuthN/AuthZ流程中產生的所有事件上，都會在使用者端提供此形式的使用者ID。 |
| 短媒體權杖的sessionGUID屬性 | 對同時使用情形的詐騙追蹤 | 是 | 是 |  — 這與透過sendTrackingData()的使用者ID相同，不過此ID經過數位簽署以保護其完整性，且足以用於詐騙追蹤。 </br> </br>  — 此影片旨在使用我們的驗證器程式庫後，於伺服器端處理，且可在向使用者端發佈影片串流之前，針對詐騙模式進行分析。  這些工作的執行由程式設計師決定。 |
| getMetadata() userID屬性 | 帳戶連結、與MVPD的詐騙調查 | 否 | 否 |  — 此屬性可讓Adobe將實際來源MVPD使用者ID公開給程式設計師。 </br> </br>  — 在Adobe的設定中，可將其設定為加密或不加密（取決於MVPD偏好設定）。 如果已加密，則會使用提供給Adobe之程式設計師憑證的公開金鑰加以加密，因此使用者端不會明確看到該金鑰。 </br> </br>  — 這可讓程式設計師從MVPD取得實際的使用者ID，因此可直接與MVPD用於帳戶連結或詐騙調查。 |


**總結**

* 一般而言，MVPD會提供永續性唯一ID <u>並在成功驗證時傳遞給Adobe</u>. 通常在所有網路上都是一致的。 Comcast MVPD是個例外，它為每個頻道提供不同的使用者ID。

* MVPD使用者ID不包含PII，且不是帳號。 它不需要以加密形式公開，因為我們已透過所有未傳送PII的MVPD進行驗證。

使用者ID的使用方式取決於使用案例：

* 如果您需要它來追蹤/分析，最實用的地方是從 `sendTrackingData()`.
* 如果您在伺服器端需要串流發佈、詐騙或操作資料的資料，可以從媒體代號驗證器取得。
* 如果您需要帳戶連結及更深入的詐騙操作，請洽詢您的Adobe聯絡人以取得相關資訊。
