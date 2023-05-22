---
title: 檢索授權令牌
description: 檢索授權令牌
exl-id: 0b010958-efa8-4dd9-b11b-5d10f51f5680
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# 檢索授權令牌 {#retrieve-authorization-token}

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

檢索授權(AuthZ)令牌。  


| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authz</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/authz | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>2.  設備ID（必需）</br>3.  資源（必需）</br>4.  device_info/X-Device-Info（必需）</br>5.  _設備類型_</br> 6。  _設備用戶_ （不建議使用）</br>7。  _應用ID_ （不建議使用） | GET | 1。成功</br>2.  驗證令牌  </br>    未找到或已過期：   </br>    XML解釋原因  </br>    找不到authn令牌</br>3.  授權令牌  </br>    未找到：  </br>    XML說明</br>4.  授權令牌  </br>    已過期：  </br>    XML說明 | 200 — 成功  </br>412 — 無身份驗證</br></br>404 — 無AuthZ</br></br>410 - AuthZ已過期 |

{style="table-layout:auto"}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、標識用戶請求的內容並由MVPD授權端點識別的字串。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->。 |
| _設備類型_ | 設備類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clientless時，可以執行不同類型的分析，例如Roku、AppleTV和Xbox。</br></br>看， [在傳遞度量中使用無客戶端設備類型參數的好處&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 |

{style="table-layout:auto"}


### 示例響應 {#response}

 

#### 成功

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authorization>
        <expires>1348148289000</expires>
        <mvpd>sampleMvpdId</mvpd>
        <requestor>sampleRequestorId</requestor>
        <resource>sampleResourceId</resource>
        <proxyMvpd>sampleProxyMvpdId</proxyMvpd>
    </authorization>
```

 

**JSON:**

```JSON
    {
        "mvpd": "sampleMvpdId",
        "resource": "sampleResourceId",
        "requestor": "sampleRequestorId",
        "expires": "1348148289000",
        "proxyMvpd": "sampleProxyMvpdId"
    }
```

 </br>


#### 未找到或過期身份驗證令牌：

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>412</status>
        <message>User not authenticated</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 412,
        "message": "User not authenticated",
        "details": null
    }
```

</br>
 

#### 找不到授權令牌：

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>404</status>
        <message>Not found</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 404,
        "message": "Not Found",
        "details": null
    }
```

</br>

 

#### 授權令牌已過期：

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <error>
        <status>410</status>
        <message>Gone</message>
    </error>
```

 

**JSON:**

```JSON
    {
        "status": 410,
        "message": "Gone",
        "details": null
    }
```
