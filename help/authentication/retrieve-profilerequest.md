---
title: 檢索平台SSO配置檔案請求
description: 檢索平台SSO配置檔案請求
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# 檢索平台SSO配置檔案請求 {#retrieve-platform-sso-profile-request}

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

此資源為請求者ID和MVPD元組生成配置檔案請求。


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{requestor/profile-requests/{mvpd} | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（路徑參數）</br>2. mvpd（路徑參數）</br>3. deviceType（必需） | GET | 響應內容類型將是application/octet-stream，因為客戶端應用程式的實際負載不透明。</br></br>應將響應轉發到平台</br></br>用於獲取簡檔SSO的SSO引擎。 | 200 — 成功   </br>400 — 錯誤請求 |


| 輸入參數 | 說明 |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| mvpd | 此操作對其有效的MVPD ID。 |
| 設備類型 | 我們正嘗試為其獲取配置檔案請求的Apple平台。  要麼 **iOS** 或 **電視作業系統**。 |

### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
