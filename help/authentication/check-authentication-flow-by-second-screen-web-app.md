---
title: 按第二螢幕Web應用檢查身份驗證流
description: 按第二螢幕Web應用檢查身份驗證流
source-git-commit: 41da00e32b83aa6ea4437f95e26598e8932c4312
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 按第二螢幕Web應用檢查身份驗證流 {#check-authentication-flow-by-second-screen-web-app}

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

## 說明 {#description}

此API應由第二個螢幕登錄Web應用使用，以確認Adobe Primetime身份驗證已確認成功從MVPD登錄。 我們建議在向最終用戶顯示成功消息之前調用此API，該消息指示他/她繼續到設備控制台以繼續工作流。


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{註冊代碼} | 登錄Web應用 | 1。註冊碼  </br>    （路徑元件）</br>2.  請求  </br>    （強制） | GET | 如果失敗，則包含錯誤詳細資訊的XML或JSON。 | 200 — 成功   </br>403 — 禁止 |

</br>

| 輸入參數 | 說明 |
| ----------------- | --------------------------------------------------------------------------------------------- |
| 註冊碼 | 用戶在驗證流開始時提供的註冊代碼值。 |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |


### 示例響應（如果出現錯誤） {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
