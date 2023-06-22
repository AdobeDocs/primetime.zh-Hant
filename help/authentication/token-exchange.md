---
title: 交換平台SSO權杖以取得Adobe權杖
description: 交換平台SSO權杖以取得Adobe權杖
exl-id: 5ab60268-8f97-4755-8281-be45e812ed7f
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 2%

---

# 交換平台SSO權杖以取得Adobe權杖 {#exchange-a-platform-sso-token-for-an-adobe-token}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## REST API端點 {#clientless-endpoints}

&lt;reggie_fqdn>：

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 分段 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>：

* 生產 —  [api.auth.adobe.com](http://api.auth.adobe.com/)
* 分段 —  [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## 說明 {#description}

允許將平台SSO設定檔「交換」為Adobe權杖。

| 端點 | 已呼叫  </br>作者： | 輸入   </br>引數 | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn | 串流應用程式</br></br>或</br></br>程式設計師服務 | 1.請求者（必要）</br>    </br>2.  deviceId （必要）</br>    </br>3.  mvpd （必要）</br>    </br>4.  deviceType （必要）</br>    </br>5.  SAMLResponse （必要）</br>    </br>6.  deviceUser （已棄用）</br>    </br>7.  appId （已棄用） | POST | 成功的回應將是「204無內容」，這表示已成功建立權杖，且已準備好用於授權流程。 | 204 — 無內容   </br>400 — 錯誤請求 |


| 輸入引數 | 說明 |
| --- | --- |
| 請求者 | 此作業有效的程式設計員requestorId。 |
| deviceId | 裝置ID位元組。 |
| mvpd | 此作業適用的MVPD ID。 |
| deviceType | 我們嘗試為其取得設定檔請求的Apple平台。  兩者之一 **iOS** 或 **tvOS**. |
| SAMLResponse | 平台SSO傳回的實際設定檔。 |
| _deviceuser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式id/名稱。 |
