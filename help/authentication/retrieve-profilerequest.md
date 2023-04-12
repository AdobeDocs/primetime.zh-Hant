---
title: 擷取Platform SSO設定檔請求
description: 擷取Platform SSO設定檔請求
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# 擷取Platform SSO設定檔請求 {#retrieve-platform-sso-profile-request}

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

此資源會產生要求者ID和MVPD元組的設定檔要求。


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor}/profile-requests/{mvpd} | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（路徑參數）</br>2. mvpd（路徑參數）</br>3. deviceType（必要） | GET | 回應Content-Type將為application/八位元資料流，因為用戶端應用程式的實際裝載不透明。</br></br>應用程式應將回應轉送至Platform</br></br>用於取得設定檔SSO的SSO引擎。 | 200 — 成功   </br>400 — 錯誤請求 |


| 輸入參數 | 說明 |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| mvpd | 此操作對其有效的MVPD ID。 |
| deviceType | 我們嘗試取得設定檔要求的Apple平台。  其中 **iOS** 或 **tvOS**. |


