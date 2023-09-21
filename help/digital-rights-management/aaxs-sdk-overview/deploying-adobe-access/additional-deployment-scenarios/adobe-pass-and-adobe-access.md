---
title: Adobe Pass與Adobe存取
description: Adobe Pass與Adobe存取
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Adobe Pass與Adobe存取 {#adobe-pass-and-adobe-access}

ADOBE PASS ( [](https://www.adobe.com/products/adobepass/))提供跨多個內容提供者的使用者/裝置驗證和授權。 使用者必須擁有有效的有線電視或衛星電視訂閱。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass可與Adobe存取搭配使用，以保護媒體內容。 在此案例中，視訊播放器(SWF)可以載入另一個SWF，稱為 *存取啟用程式*，由Adobe Systems託管。 此 *存取啟用程式* 用於連線至Adobe Pass服務，並促進SAML SSO與MVPD的（多頻道視訊程式設計經銷商）身分提供者系統的整合。 這包括將使用者的瀏覽器短暫重新導向至MVPD登入頁面，然後保留AuthN權杖，最後以快取的AuthN工作階段返回內容網站。

此 *存取啟用程式* 然後可以促進Adobe Pass服務和MVPD之間的後端授權。 MVPD會維護商業邏輯，並決定使用者有權使用的內容。 權利會保留在該內容資源的額外AuthZ權杖中，並傳回給使用者端。

驗證和授權權杖使用Adobe存取使用者端的唯一ID和私密金鑰簽署，以避免竄改或詐騙。 此Token只能透過 *存取啟用程式*.

視訊播放器可藉由呼叫 `getAuthorization` 於 *存取啟用程式*. 當有效的AuthN/AuthZ權杖出現時， *AccessEnabler* 發出回撥給視訊播放器，其中包含播放視訊內容的短期媒體權杖。

Adobe Pass提供可部署至伺服器的媒體權杖驗證器Java程式庫。 使用Flass Access伺服器進行內容保護時，您可以將媒體權杖驗證器與Adobe存取伺服器端外掛程式整合，以便在成功驗證媒體權杖後自動發行通用授權。 然後內容會從CDN伺服器串流至使用者端。 若要取得內容授權，可將短暫的媒體權杖提交至Adobe存取伺服器，在該伺服器會驗證權杖的有效性並可核發授權。

長效的AuthN代號通常會由 *存取啟用程式* 以代表該MVPD訂閱者的AuthN。 此外，Adobe Access Server和權杖驗證器可由CDN或服務提供者（代表內容提供者）操作。
