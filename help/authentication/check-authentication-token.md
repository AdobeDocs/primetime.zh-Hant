---
title: 檢查驗證令牌
description: 檢查驗證令牌
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 2%

---


# 檢查驗證令牌 {#check-authentication-token}

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

指示設備是否具有未到期的身份驗證令牌。

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/checkauthn | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>2.  設備ID（必需）</br>3.  device_info/X-Device-Info（必需）</br>4.  _設備類型_ </br>5.  _設備用戶_ （不建議使用）</br>6。  _應用ID_ （不建議使用） | GET | 如果失敗，則包含錯誤詳細資訊的XML或JSON。 | 200 — 成功   </br>403 — 未成功 |

{style=&quot;table-layout:auto&quot;}


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br>請參閱中的完整詳細資訊 [傳遞設備和連接資訊](http://tve.helpdocsonline.com/passing-device-information)。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。 |
| _應用ID_ | 應用程式ID/名稱。</br>**注釋**:device_info將替換此參數。 |

{style=&quot;table-layout:auto&quot;&quot;


## 響應（如果不成功） {#response}

```JSON
    <error>
      <status>403</status>
      <message>Authentication token expired</message>
    </error>
```

### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
