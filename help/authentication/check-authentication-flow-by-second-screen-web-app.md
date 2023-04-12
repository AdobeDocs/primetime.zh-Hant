---
title: 按第二螢幕Web應用檢查驗證流
description: 按第二螢幕Web應用檢查驗證流
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 按第二螢幕Web應用檢查驗證流 {#check-authentication-flow-by-second-screen-web-app}

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

## 說明 {#description}

第二個螢幕登入Web應用程式應使用此API，以確認Adobe Primetime驗證已確認已從MVPD成功登入。 建議您先呼叫此API，再向使用者顯示成功訊息，指示他/她繼續前往裝置主控台，繼續執行工作流程。


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{registration code} | 登入網頁應用程式 | 1.註冊代碼  </br>    （路徑元件）</br>2.  請求者  </br>    （強制） | GET | 如果失敗，則包含錯誤詳細資料的XML或JSON。 | 200 — 成功   </br>403 — 禁止 |

</br>

| 輸入參數 | 說明 |
| ----------------- | --------------------------------------------------------------------------------------------- |
| 註冊代碼 | 用戶在驗證流程開始時提供的註冊代碼值。 |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |


### 範例回應（若發生錯誤） {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [返回REST API參考](/help/authentication/rest-api-reference.md)
