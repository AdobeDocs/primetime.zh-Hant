---
title: REST API參考
description: Rest api參考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---


# REST API參考 {#rest-api-reference}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 回應格式 {#response-formats}


>[!NOTE]
>
> 這些服務中提供的API可傳回XML或JSON的回應（適用於傳回回應的API）。 在請求中指定回應格式有3種不同方式：
>
>* 將HTTP Accept Header設定為 `application/xml` 或 `application/json`.
>* 在要求裝載中，指定參數 `format=xml` 或 `format=json`.
>* 使用擴充功能呼叫Web服務端點 `.xml` 或 `.json`. 例如， `/regcode.xml` 或 `/regcode.json`
>
>您可以指定上述方法的任何一個。 指定具有衝突格式的多個方法可能導致錯誤或不期望的輸出。

## 重設API端點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 網站服務摘要 {#web_srvs_summary}

下表列出了無客戶端方法的可用Web服務。 按一下網站服務端點以取得詳細資訊（範例要求和回應、輸入參數、HTTP方法等）


| Sr | Web服務端點 | 說明 | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | 托管於 | 呼叫者 |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | 返回隨機生成的註冊代碼和登錄頁URI | 2 | Adobe  </br>註冊代碼服務 | 智慧裝置 |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | 傳回包含註冊代碼UUID、註冊代碼和雜湊裝置ID的註冊代碼記錄 | 8 | Adobe  </br>註冊代碼服務 | Primetime驗證 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | 傳回要求者已設定的MVPD清單 | 5 | Adobe  </br>Primetime  </br>驗證  </br>服務 | 登入  </br>Web  </br>應用程式 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](/help/authentication/initiate-authentication.md) | 通知MVPD選取事件以啟動AuthN程式。 在驗證資料庫上建立記錄，當從MVPD收到成功回應時進行調解（步驟13） | 7 | Adobe  </br>Primetime  </br>驗證  </br>服務 | 登入  </br>Web  </br>應用程式 |
| 5. | SAML斷言使用者 | Primetime驗證和MVPD之間的現有SAML工作流程 | 13 | Primetime  </br>驗證  </br>服務 | Primetime驗證 |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | 登入Web應用程式可檢查嘗試的登入流程是否成功 |  | Primetime  </br>驗證   </br>服務 | 登入   </br>Web   </br>應用程式 |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | 取得AuthN代號相關中繼資料 | 15 | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | 刪除登錄代碼記錄併發行登錄代碼以供重複使用 | 16 | Adobe  </br>註冊代碼服務 | Primetime驗證 |
| 9. | [&lt;sp_fqdn>/api/v1/authorize](/help/authentication/initiate-authorization.md) | 獲取授權響應。 | 17 | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | 指出裝置是否有未過期的AuthN代號。 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | 若找到AuthN代號，則傳回該代號。 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | 若找到AuthZ代號，則傳回該代號。 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | 若找到短媒體代號，則傳回 — 與/api/v1/mediatoken相同 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | 取得短媒體代號 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorize](/help/authentication/retrieve-list-of-preauthorized-resources.md) | 檢索預授權資源的清單 |  | Primetime  </br>驗證  </br>服務 | 智慧裝置 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorize/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | 擷取預先授權的資源清單 |  | Primetime  </br>驗證  </br>服務 | 登入網頁應用程式 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](/help/authentication/initiate-logout.md) | 從儲存中移除AuthN和AuthZ代號 |  | Primetime  </br>驗證   </br>服務 | 智慧裝置 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | 驗證流程完成後獲取用戶元資料 | 不適用 | 不適用 | 智慧裝置 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | 為Temp Pass或Promotion Temp Pass建立驗證Token | 不適用 | Primetime  </br>驗證  </br>服務 | 智慧裝置 |


## REST API安全性 {#security}

所有Primetime驗證無用戶端API都必須使用HTTPS通訊協定來呼叫，才能進行安全通訊。 此外，呼叫的大部分API都應包含 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md).

