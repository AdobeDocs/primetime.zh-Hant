---
title: 檢索身份驗證令牌
description: 檢索身份驗證令牌
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 2%

---


# 檢索身份驗證令牌 {#retrieve-authentication-token}

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

檢索身份驗證(AuthN)令牌。  

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/tokens/authn</br></br>例如：</br></br>&lt;sp_fqdn>/api/v1/tokens/authn | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>2.  設備ID（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  _設備類型_ （已棄用）</br>5.  _設備用戶_ （不建議使用）</br>6。  _應用ID_ （不建議使用） | GET | 包含驗證資訊或錯誤詳細資訊（如果失敗）的XML或JSON。 | 200 — 成功。  </br>404 — 未找到令牌  </br>410 — 令牌已過期 |

{style=&quot;table-layout:auto&quot;}


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br>請參閱中的完整詳細資訊 [傳遞設備和連接資訊](http://tve.helpdocsonline.com/passing-device-information)。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。</br></br>**注釋**：如果使用，則deviceUser的值應與 [建立註冊代碼](http://tve.helpdocsonline.com/registration-code-request) 請求。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 如果使用， `appId` 應具有與 [建立註冊代碼](http://tve.helpdocsonline.com/registration-code-request) 請求。 |

{style=&quot;table-layout:auto&quot;&quot;

</br>

### 示例響應 {#response}

 

#### 成功

**XML:**

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <authentication>
         <expires>1601114932000</expires>
         <userId>sampleUserId</userId>
         <mvpd>sampleMvpdId</mvpd>
         <requestor>sampleRequestor</requestor>
    </authentication>
```


**JSON:**

```JSON
    {
         "requestor": "sampleRequestor",
         "mvpd": "sampleMvpdId",
         "userId": "sampleUserId",
         "expires": "1601114932000"
    }
```

 

 

#### 找不到身份驗證令牌：

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
        "message": "Not Found"
    }
```

[返回無客戶端API參考](http://tve.helpdocsonline.com/clientless-api-reference)
