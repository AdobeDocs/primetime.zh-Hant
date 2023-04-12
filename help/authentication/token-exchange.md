---
title: 為Adobe代號交換平台SSO代號
description: 為Adobe代號交換平台SSO代號
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---


# 為Adobe代號交換平台SSO代號 {#exchange-a-platform-sso-token-for-an-adobe-token}

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

允許以「交換」Platform SSO設定檔來取得AdobeToken。

| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（強制）</br>    </br>2.  deviceId（必要）</br>    </br>3.  mvpd（必要）</br>    </br>4.  deviceType（必要）</br>    </br>5.  SAMLResponse（強制）</br>    </br>6.  deviceUser（已過時）</br>    </br>7.  appId（已過時） | POST | 成功的回應將是「204無內容」，表示Token已成功建立，且已準備好用於驗證流程。 | 204 — 無內容   </br>400 — 錯誤請求 |


| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| mvpd | 此操作對其有效的MVPD ID。 |
| deviceType | 我們嘗試取得設定檔要求的Apple平台。  其中 **iOS** 或 **tvOS**. |
| SAMLResponse | Platform SSO傳回的實際設定檔。 |
| _deviceUser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式ID/名稱。 |


