---
seo-title: Adobe Primetime驗證與Adobe Primetime DRM
title: Adobe Primetime驗證與Adobe Primetime DRM
uuid: 44fe3956-efb5-4fc5-97e2-37abb6554322
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Adobe Primetime驗證與Adobe Primetime DRM {#adobe-primetime-authentication-and-adobe-primetime-drm}

Adobe Primetime驗證( [https://www.adobe.com/products/adobepass/](https://www.adobe.com/products/adobepass/))可跨多個內容提供者提供使用者／裝置驗證和授權。 使用者必須有有效的有線電視或衛星電視訂閱。

<!--<a id="fig_cln_bc2_44"></a>-->

![](assets/AdobePass_web.png)

Adobe Primetime驗證可與Adobe Primetime DRM搭配使用，以保護媒體內容。 在此案例中，視訊播放器(SWF)可載入另一個名為 *Access Enabler*，由Adobe Systems代管的SWF。 Access Enabler *(* Access Enabler)可用來連線至Adobe Primetime驗證服務，並協助SAML SSO與MVPD（多頻道視訊程式設計代理商）身分提供者系統整合。 這包括將使用者的瀏覽器短暫重新導向至MVPD登入頁面，然後保留AuthN Token，最後以快取的AuthN工作階段返回內容網站。

然後 *Access Enabler* 便可協助Adobe Primetime驗證服務和MVPD之間的後端授權。 MVPD會維護商業邏輯，並決定使用者有權使用哪些內容。 權益會持續存在該內容資源的額外AuthZ Token中，並傳回給用戶端。

驗證和授權Token使用Primetime DRM用戶端的唯一ID和私密金鑰進行簽署，以避免竄改或欺騙。 此標籤只能通過 *Access Enabler訪問*。

視訊播放器可以呼叫Access Enabler來 `getAuthorization` 觸發 *程式*。 當有效的AuthN/AuthZ代號存在時， *AccessEnabler* 會向視訊播放器發出回呼，該回呼將包含用於播放視訊內容的短期媒體代號。

Adobe Primetime驗證提供可部署至伺服器的媒體Token驗證器Java程式庫。 當使用Primetime DRM伺服器進行內容保護時，您可將媒體Token驗證器與Primetime DRM伺服器端外掛程式整合，以在成功驗證媒體Token後自動發行一般授權。 然後內容從CDN伺服器串流至用戶端。 為了獲得內容許可，可將短期媒體令牌提交到Primetime DRM伺服器，其中驗證令牌的有效性並可發放許可。

Access Enabler通常會在所有內容開發人員中使用長壽命的 *AuthN Token* ，代表該MVPD訂閱者的AuthN。 此外，Primetime DRM伺服器和Token驗證器可由CDN或服務供應商代表內容供應商操作。