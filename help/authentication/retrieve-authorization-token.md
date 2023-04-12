---
title: 擷取授權Token
description: 擷取授權Token
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# 擷取授權Token {#retrieve-authorization-token}

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

擷取授權(AuthZ)Token。  


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authz</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/authz | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（強制）</br>2.  deviceId（必要）</br>3.  資源（必要）</br>4.  device_info/X-Device-Info（強制）</br>5。  _deviceType_</br> 6.  _deviceUser_ （已過時）</br>7.  _appId_ （已過時） | GET | 1.成功</br>2.  驗證Token  </br>    找不到或已過期：   </br>    XML解釋原因  </br>    找不到authn令牌</br>3.  授權Token  </br>    找不到：  </br>    XML說明</br>4.  授權Token  </br>    已過期：  </br>    XML說明 | 200 — 成功  </br>412 — 無驗證</br></br>404 — 無AuthZ</br></br>410 - AuthZ已過期 |

{style="table-layout:auto"}

</br>

| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、識別使用者要求的內容並由MVPD授權端點識別的字串。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便執行不同類型的分析，例如Roku、AppleTV和Xbox。</br></br>看， [在傳遞量度中使用無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 |

{style="table-layout:auto"}


### 範例回應 {#response}

 

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


#### 未找到或已過期驗證令牌：

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
 

#### 未找到授權令牌：

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

 

#### 授權Token已過期：

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
