---
title: Adobe Pass與Adobe
description: Adobe Pass與Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---


# Adobe Pass和Adobe訪問{#adobe-pass-and-adobe-access}

Adobe Pass([](https://www.adobe.com/products/adobepass/))提供多個內容提供者的使用者／裝置驗證和授權。 使用者必須有有效的有線電視或衛星電視訂閱。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Pass可與Adobe存取一起使用，以保護媒體內容。 在此案例中，視訊播放器(SWF)可載入另一個名為&#x200B;*Access Enabler*&#x200B;的SWF，由Adobe Systems代管。 *Access Enabler*&#x200B;用於連接Adobe Pass服務，並促進SAML SSO與MVPD（多通道視訊程式設計代理商）身分提供者系統的整合。 這包括將使用者的瀏覽器短暫重新導向至MVPD登入頁面，然後保留AuthN Token，最後以快取的AuthN工作階段返回內容網站。

然後，*Access Enabler*&#x200B;便於在Adobe Pass服務和MVPD之間進行後端授權。 MVPD會維護商業邏輯，並決定使用者有權使用哪些內容。 權益會持續存在該內容資源的額外AuthZ Token中，並傳回給用戶端。

驗證和授權Token使用Adobe存取用戶端的唯一ID和私密金鑰進行簽署，以避免竄改或欺騙。 此標籤只能通過&#x200B;*Access Enabler*&#x200B;訪問。

視頻播放器可通過調用&#x200B;*Access Enabler*&#x200B;上的`getAuthorization`來觸發該過程。 當存在有效的AuthN/AuthZ代號時，*AccessEnabler*&#x200B;會向視訊播放器發出回呼，該回呼將包含用於播放視訊內容的短期媒體代號。

Adobe Pass提供可部署至伺服器的媒體Token驗證器Java程式庫。 當使用Flash Access伺服器進行內容保護時，您可將媒體Token驗證器與AdobeAccess伺服器端外掛程式整合，以在成功驗證媒體Token後自動發行一般授權。 然後內容從CDN伺服器串流至用戶端。 為了獲得內容許可，可將短壽命媒體令牌提交到Adobe訪問伺服器，其中驗證令牌的有效性並可頒發許可證。

長壽命的AuthN代號通常由&#x200B;*存取啟用碼*&#x200B;所有內容開發人員使用，以代表該MVPD訂閱者的AuthN。 此外，Adobe Access Server和令牌驗證器可由CDN或服務提供商代表內容提供商操作。
