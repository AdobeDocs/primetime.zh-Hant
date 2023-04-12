---
title: 取得短媒體代號
description: 取得短媒體權杖
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# 取得短媒體代號 {#obtain-short-media-token}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 重設API端點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 測試 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 測試 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## 說明 {#description}

取得短媒體代號。  

| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediatoken</br></br>  或</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/media | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（強制）</br>2.  deviceId（必要）</br>3.  資源（必要）</br>4.  device_info/X-Device-Info（強制）</br>5。  _deviceType_</br> 6.  _deviceUser_ （已過時）</br>7.  _appId_ （已過時） | GET | 包含Base64編碼媒體代號的XML或JSON，若失敗則顯示錯誤詳細資訊。 | 200 — 成功  </br>403 — 沒有成功 |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、識別使用者要求的內容並由MVPD授權端點識別的字串。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br>請參閱 [傳遞裝置和連線資訊](/help/authentication/passing-client-information-device-connection-and-application.md). |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type)，以便針對執行不同類型的分析。 例如Roku、AppleTV和Xbox。</br></br>請參閱 [使用無客戶端設備類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。</br></br>**附註**:若已使用，deviceUser的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 若已使用， `appId` 的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |

{style="table-layout:auto"}

### 範例回應 {#response}

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <play>
        <expires>1348649569000</expires>
        <mvpdId>sampleMvpdId</mvpdId>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <serializedToken>PHNpZ25hdH[...]</serializedToken>
        <userId>sampleScrambledUserId</userId>
    </play>
```



**JSON:**

```JSON
    {
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348649614000",
        "serializedToken": "PHNpZ25hdH[...]",
        "userId": "sampleScrambledUserId",
        "mvpdId": "sampleMvpdId"
    }
```

 

### 媒體驗證庫相容性

欄位 `serializedToken` 從「取得短媒體代號」呼叫是Base64編碼代號，可根據Adobe Medium驗證程式庫驗證。
