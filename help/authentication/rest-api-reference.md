---
title: REST API參考
description: Rest api引用
exl-id: 67e4639e-db0b-4400-bb81-e214263e8395
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# REST API參考 {#rest-api-reference}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 響應格式 {#response-formats}


>[!NOTE]
>
> 這些服務中提供的API可以以XML或JSON返迴響應（對於返迴響應的API）。 在請求中指定響應格式有三種不同的方法：
>
>* 將HTTP接受標頭設定為 `application/xml` 或 `application/json`。
>* 在請求負載中，指定參數 `format=xml` 或 `format=json`。
>* 使用擴展調用Web服務終結點 `.xml` 或 `.json`。 比如說， `/regcode.xml` 或 `/regcode.json`
>
>可以指定以上方法中的任何一種。 指定具有衝突格式的多個方法可能會導致錯誤或不期望的輸出。

## REST API終結點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Web服務摘要 {#web_srvs_summary}

下表列出了無客戶端方法的可用Web服務。 按一下Web服務端點以瞭解詳細資訊（示例請求和響應、輸入參數、HTTP方法等）


| 老 | Web服務終結點 | 說明 | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | 托管於 | 調用者 |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | 返回隨機生成的註冊代碼和登錄頁URI | 2 | Adobe  </br>註冊代碼服務 | 智慧設備 |
| 2. | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | 返回包含註冊代碼UUID、註冊代碼和散列設備ID的註冊代碼記錄 | 8 | Adobe  </br>註冊代碼服務 | 黃金時段驗證 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | 返回請求方的已配置MVPD清單 | 5 | Adobe  </br>黃金時段  </br>認證  </br>服務 | 登錄  </br>Web  </br>應用 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](/help/authentication/initiate-authentication.md) | 通過通知MVPD選擇事件啟動AuthN進程。 在驗證資料庫上建立記錄，當從MVPD接收成功響應時對其進行協調（步驟13） | 7 | Adobe  </br>黃金時段  </br>認證  </br>服務 | 登錄  </br>Web  </br>應用 |
| 5. | SAML斷言使用者 | Mogini時驗證和MVPD之間的現有SAML工作流 | 13 | 黃金時段  </br>認證  </br>服務 | 黃金時段驗證 |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | 登錄Web應用可以檢查嘗試的登錄流是否成功 |  | 黃金時段  </br>認證   </br>服務 | 登錄   </br>Web   </br>應用 |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | 獲取與AuthN令牌相關的元資料 | 15 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 8. | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | 刪除註冊碼記錄並釋放註冊碼以供重用 | 16 | Adobe  </br>註冊代碼服務 | 黃金時段驗證 |
| 9. | [&lt;sp_fqdn>/api/v1/authorize](/help/authentication/initiate-authorization.md) | 獲取授權響應。 | 17 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | 指示設備是否具有未到期的AuthN令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | 如果找到，則返回AuthN令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | 如果找到，則返回AuthZ令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | 返回短媒體令牌（如果找到） — 與/api/v1/mediatoken相同 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 14. | [&lt;sp_fqdn>/api/v1/mediaken](/help/authentication/obtain-short-media-token.md) | 獲取短媒體令牌 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorize](/help/authentication/retrieve-list-of-preauthorized-resources.md) | 檢索預授權資源清單 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorize/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | 檢索預授權資源清單 |  | 黃金時段  </br>認證  </br>服務 | 登錄Web應用 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](/help/authentication/initiate-logout.md) | 從儲存中刪除AuthN和AuthZ令牌 |  | 黃金時段  </br>認證   </br>服務 | 智慧設備 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | 在驗證流完成後獲取用戶元資料 | 不適用 | 不適用 | 智慧設備 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | 為臨時傳遞或提升臨時傳遞建立驗證令牌 | 不適用 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |


## REST API安全 {#security}

必須使用HTTPS協定調用所有黃金時段驗證無客戶端API，以實現安全通信。 此外，調用的大多數API應包含由 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)。
