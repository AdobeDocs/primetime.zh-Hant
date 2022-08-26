---
title: REST API參考
description: Rest api引用
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
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
>* 將HTTP接受標頭設定為「application/xml」</code>&quot;或&quot;application/json</code>&quot;
>* 在請求負載中，指定參數&quot;format=xml</code>&quot;或&quot;format=json</code>&quot;</li>
>* 使用副檔名.xml調用Web服務終結點</code> 或.json</code>。 例如，「/regcode.xml」</code>&quot;或&quot;/regcode.json&quot;</code>&quot;
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


| 老 | Web服務終結點 | 說明 | [迪亞格。  </br>參考](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)。 | 托管於 | 調用者 |
| --- | --- | --- | --- | --- | --- |
| 1。 | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | 返回隨機生成的註冊代碼和登錄頁URI | 2 | Adobe  </br>註冊代碼服務 | 智慧設備 |
| 2. | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | 返回包含註冊代碼UUID、註冊代碼和散列設備ID的註冊代碼記錄 | 8 | Adobe  </br>註冊代碼服務 | 黃金時段驗證 |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | 返回請求方的已配置MVPD清單 | 5 | Adobe  </br>黃金時段  </br>認證  </br>服務 | 登錄  </br>Web  </br>應用 |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](http://tve.helpdocsonline.com/initiate-authentication) | 通過通知MVPD選擇事件啟動AuthN進程。 在驗證資料庫上建立記錄，當從MVPD接收成功響應時對其進行協調（步驟13） | 7 | Adobe  </br>黃金時段  </br>認證  </br>服務 | 登錄  </br>Web  </br>應用 |
| 5. | SAML斷言使用者 | Mogini時驗證和MVPD之間的現有SAML工作流 | 13 | 黃金時段  </br>認證  </br>服務 | 黃金時段驗證 |
| 6。 | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | 登錄Web應用可以檢查嘗試的登錄流是否成功 |  | 黃金時段  </br>認證   </br>服務 | 登錄   </br>Web   </br>應用 |
| 7。 | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | 獲取與AuthN令牌相關的元資料 | 15 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 8. | [&lt;reggie_fqdn>/reggie/v1  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | 刪除註冊碼記錄並釋放註冊碼以供重用 | 16 | Adobe  </br>註冊代碼服務 | 黃金時段驗證 |
| 9。 | [&lt;sp_fqdn>/api/v1/authorize](http://tve.helpdocsonline.com/initiate-authorization) | 獲取授權響應。 | 17 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | 指示設備是否具有未到期的AuthN令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | 如果找到，則返回AuthN令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | 如果找到，則返回AuthZ令牌。 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | 返回短媒體令牌（如果找到） — 與/api/v1/mediatoken相同 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 14. | [&lt;sp_fqdn>/api/v1/mediaken](http://tve.helpdocsonline.com/obtain-short-media-token) | 獲取短媒體令牌 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorize](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | 檢索預授權資源清單 |  | 黃金時段  </br>認證  </br>服務 | 智慧設備 |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorize/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | 檢索預授權資源清單 |  | 黃金時段  </br>認證  </br>服務 | 登錄Web應用 |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | 從儲存中刪除AuthN和AuthZ令牌 |  | 黃金時段  </br>認證   </br>服務 | 智慧設備 |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | 在驗證流完成後獲取用戶元資料 | 不適用 | 不適用 | 智慧設備 |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | 為臨時傳遞或提升臨時傳遞建立驗證令牌 | 不適用 | 黃金時段  </br>認證  </br>服務 | 智慧設備 |

{style=&quot;table-layout:auto&quot;}

## REST API安全 {#security}

必須使用HTTPS協定調用所有黃金時段驗證無客戶端API，以實現安全通信。 此外，調用的大多數API應包含由 [動態客戶端註冊](http://tve.helpdocsonline.com/dynamic-client-registration)。


## 相關資訊 {#related}

* [REST API概述](http://tve.helpdocsonline.com/reset-api-overview)
* [伺服器到伺服器指南](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [客戶端到伺服器指南](http://tve.helpdocsonline.com/client-to-server)
* [避免在/authenticate請求中使用&#39;&amp;&#39;reg\_code（技術說明）](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
