---
title: 為Adobe令牌交換平台SSO令牌
description: 為Adobe令牌交換平台SSO令牌
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 2%

---


# 為Adobe令牌交換平台SSO令牌 {#exchange-a-platform-sso-token-for-an-adobe-token}

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

允許將平台SSO配置檔案「交換」為Adobe令牌。

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>    </br>2.  設備ID（必需）</br>    </br>3.  mvpd（必需）</br>    </br>4.  deviceType（必需）</br>    </br>5.  SAMLResponse（強制）</br>    </br>6。  deviceUser（不建議使用）</br>    </br>7。  appId（不建議使用） | POST | 成功的響應將是204無內容，表示令牌已成功建立並準備用於驗證流。 | 204 — 無內容   </br>400 — 錯誤請求 |


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| mvpd | 此操作對其有效的MVPD ID。 |
| 設備類型 | 我們正嘗試為其獲取配置檔案請求的Apple平台。  要麼 **iOS** 或 **電視作業系統**。 |
| 薩姆勒埃斯龐塞 | 平台SSO返回的實際配置檔案。 |
| _設備用戶_ | 設備用戶標識符。 |
| _應用ID_ | 應用程式ID/名稱。 |



### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
