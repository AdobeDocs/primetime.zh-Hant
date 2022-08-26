---
title: 刪除註冊記錄
description: 刪除註冊資源
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 4%

---


# 刪除註冊記錄 {#delete-registration-record}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## REST API終結點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 暫存 —  [api.auth.staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## 說明 {#delete-record}

刪除註冊碼記錄並釋放註冊碼以供重用。 

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>例如：</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45TRY | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者ID  </br>    （路徑元件）</br>2.  註冊代碼  </br>    （路徑元件） | DELETE | 無 | 204 |

{style=&quot;table-layout:auto&quot;}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 註冊碼 | 將顯示在流設備（要輸入到驗證流）上的註冊代碼值。 |

{style=&quot;table-layout:auto&quot;&quot;

</br>

### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
