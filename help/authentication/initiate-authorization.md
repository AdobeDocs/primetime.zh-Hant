---
title: 啟動授權
description: 啟動授權
exl-id: 2f8a5499-e94f-40dd-9fb0-aac8e080de66
source-git-commit: 5e775238f0e894f887be4c188903bdb04524c57a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 啟動授權 {#initiate-authorization}

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

獲取授權響應。 

| 端點 | 已調用  </br>按 | 輸入   </br>帕拉姆 | HTTP  </br>方法 | 響應 | HTTP  </br>響應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorize | 流式處理應用</br></br>或</br></br>程式設計師服務 | 1。請求者（必需）</br>2.  設備ID（必需）</br>3.  資源（必需）</br>4.  device_info/X-Device-Info（必需）</br>5.  _設備類型_</br> 6。  _設備用戶_ （不建議使用）</br>7。  _應用ID_ （不建議使用）</br>8.  額外參數（可選） | GET | 包含授權詳細資訊或錯誤詳細資訊（如果失敗）的XML或JSON。 請參見下面的示例。 | 200 — 成功  </br>403 — 未成功 |

{style="table-layout:auto"}

</br>


| 輸入參數 | 說明 |
| --- | --- |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 設備ID | 設備ID位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、標識用戶請求的內容並由MVPD授權端點識別的字串。 |
| 設備資訊/</br></br>X設備資訊 | 流設備資訊。</br></br>**注釋**:此URL可以作為URL參數傳遞，但由於此參數的可能大小和對GETURL長度的限制，它應作為X-Device-Info在http標頭中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->。 |
| _設備類型_ | 設備類型（如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供 [按設備類型分解](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用Clientless時，可對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [傳遞度量中無客戶端設備類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**注釋**:device_info將替換此參數。 |
| _設備用戶_ | 設備用戶標識符。 |
| _應用ID_ | 應用程式ID/名稱。 </br></br>**注釋**:device_info將替換此參數。 |
| 額外參數 | 該調用還可包含啟用其他功能的可選參數，如：</br></br>* generic_data — 啟用 [促銷臨時傳遞](/help/authentication/promotional-temp-pass.md)</br></br>示例： `generic_data=("email":"email@domain.com")` |

{style="table-layout:auto"}

>[!CAUTION]
>
>**流設備IP地址**</br>
>對於客戶端到伺服器實現，流設備IP地址隨此調用隱式發送。  對於伺服器到伺服器實施， **重碼** 調用由程式設計師服務而非流式設備進行，要傳遞流式設備IP地址，需要以下報頭：</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>何處 `<streaming\_device\_ip>` 是流設備公共IP地址。</br></br>
>示例：</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### 示例響應 {#sample-response}

* **案例1:成功**

</br>
  **XML:**
  </br>

    &quot;`XML
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot; standalone=&quot;yes&quot;?>
    &lt;authorization>
    &lt;expires>1348148289000&lt;/expires>
    &lt;mvpd>示例MvpdId&lt;/mvpd>
    &lt;requestor>示例請求者ID&lt;/requestor>
    &lt;resource>示例資源ID&lt;/resource>
    &lt;/authorization>
    「」



* **JSON:**

   ```JSON
   {
     "mvpd": "sampleMvpdId",
     "resource": "sampleResourceId",
     "requestor": "sampleRequestorId",
     "expires": "1348148289000"
   }
   ```

>[!IMPORTANT]
>
>當響應來自代理MVPD時，它可能包含名為 `proxyMvpd`。 

 

* **案例二：授權被拒絕**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```
