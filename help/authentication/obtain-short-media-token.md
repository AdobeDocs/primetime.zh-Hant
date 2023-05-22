---
title: 獲取短媒體令牌
description: 獲取短媒體令牌
exl-id: 667eaaba-423e-4d54-9dbe-084b3c049e1f
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 獲取短媒體令牌 {#obtain-short-media-token}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## REST API終結點 {#clientless-endpoints}

&lt;reggie_fqdn>:

* 生產 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 暫存 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* 生產 —  [`api.auth.adobe.com`](http://api.auth.adobe.com/)
* 暫存 —  [`api.auth-staging.adobe.com`](http://api.auth-staging.adobe.com/)

</br>

## 說明 {#description}

獲取短媒體令牌。  

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/mediaken</br></br>  或</br></br>&lt;sp_fqdn>/api/v1/tokens/media</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/media | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>2.  設備ID（必需）</br>3.  資源（必需）</br>4.  device_info/X-Device-Info（必需）</br>5.  _設備類型_</br> 6。  _設備用戶_ （不建議使用）</br>7。  _應用ID_ （不建議使用） | GET | 包含Base64編碼的媒體令牌的XML或JSON或錯誤詳細資訊（如果失敗）。 | 200 — 成功  </br>403 — 未成功 |

{style="table-layout:auto"}

<!--
| Endpoint | Called  </br>By | Input   </br>Params | HTTP  </br>Method | Response | HTTP  </br>Response |
| --- | --- | --- | --- | --- | --- |
| `<SP_FQDN>/api/v1/mediatoken`</br></br>  or</br></br>`<SP_FQDN>/api/v1/tokens/media`</br></br>For example:</br></br>`<SP_FQDN>/api/v1/tokens/media` | Streaming App</br></br>or</br></br>Programmer Service | <ol><li>requestor (Mandatory)</l><li>deviceId (Mandatory)</li><li>resource (Mandatory)</li><li>device_info/X-Device-Info (Mandatory)</li><li>_deviceType_</li><li>_deviceUser_ (Deprecated)</li><li>_appId_ (Deprecated)</li></ol> | GET | XML or JSON containing an Base64 encoded media token or error details if unsuccessful. | 200 - Success  </br>403 - No Success |
-->

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、標識用戶請求的內容並由MVPD授權端點識別的字串。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br>請參閱中的完整詳細資訊 [傳遞設備和連接資訊](/help/authentication/passing-client-information-device-connection-and-application.md)。 |
| _設備類型_ | 設備類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解]/(help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type)，以便可以為執行不同類型的分析。 例如， Roku、AppleTV和Xbox。</br></br>請參閱 [使用無客戶端設備類型參數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。</br></br>**注釋**:如果使用，則deviceUser的值應與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 如果使用， `appId` 應具有與 [建立註冊代碼](/help/authentication/registration-code-request.md) 請求。 |

{style="table-layout:auto"}

### 示例響應 {#response}

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

欄位 `serializedToken` 來自「獲取短媒體令牌」調用的是Base64編碼令牌，可以通過Adobe Medium驗證庫驗證。
