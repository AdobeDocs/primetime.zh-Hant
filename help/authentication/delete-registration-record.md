---
title: 刪除註冊記錄
description: 刪除註冊資源d
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 刪除註冊記錄 {#delete-registration-record}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 重設API端點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 測試 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 說明 {#delete-record}

刪除登錄代碼記錄併發行登錄代碼以供重複使用。 

| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>例如：</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.要求者ID  </br>    （路徑元件）</br>2.  註冊代碼  </br>    （路徑元件） | DELETE | 無 | 204 |

{style="table-layout:auto"}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| 註冊代碼 | 顯示在串流裝置上的註冊代碼值（要輸入驗證流程）。 |

{style="table-layout:auto"}

</br>

### [返回REST API參考](/help/authentication/rest-api-reference.md)
