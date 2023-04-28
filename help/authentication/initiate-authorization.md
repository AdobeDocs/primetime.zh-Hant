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

獲取授權響應。 

| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authorize | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（強制）</br>2.  deviceId（必要）</br>3.  資源（必要）</br>4.  device_info/X-Device-Info（強制）</br>5。  _deviceType_</br> 6.  _deviceUser_ （已過時）</br>7.  _appId_ （已過時）</br>8.  額外參數（可選） | GET | 包含授權詳細資料或錯誤詳細資料（若失敗）的XML或JSON。 請參閱以下範例。 | 200 — 成功  </br>403 — 沒有成功 |

{style="table-layout:auto"}

</br>


| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| 資源 | 包含resourceId（或MRSS片段）、識別使用者要求的內容並由MVPD授權端點識別的字串。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便可以針對Roku、AppleTV、Xbox等執行不同類型的分析。</br></br>請參閱 [傳遞量度中無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:device_info將替換此參數。 |
| _deviceUser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 |
| 額外參數 | 呼叫也可包含可啟用其他功能的選用參數，例如：</br></br>* generic_data — 啟用使用 [促銷TempPass](/help/authentication/promotional-temp-pass.md)</br></br>範例： `generic_data=("email":"email@domain.com")` |

{style="table-layout:auto"}

>[!CAUTION]
>
>**串流裝置IP位址**</br>
>對於用戶端對伺服器實作，串流裝置IP位址會以此呼叫隱式傳送。  針對伺服器對伺服器實作，其中 **regcode** 呼叫是由程式設計人員服務而非流式設備進行，需要以下標頭才能傳遞流式設備IP地址：</br></br>
>
>
```
>X-Forwarded-For : <streaming\_device\_ip>
>```
>
>where `<streaming\_device\_ip>` 是串流裝置的公用IP位址。</br></br>
>範例：</br>
>
>
```
>POST /reggie/v1/{req_id}/regcode HTTP/1.1
>X-Forwarded-For:203.45.101.20
>```


### 範例回應 {#sample-response}

* **案例1:成功**

</br>
  * **XML:**
  </br>

    &quot;&#39;XML
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot; standalone=&quot;yes&quot;?>
    &lt;authorization>
    &lt;expires>1348148289000&lt;/expires>
    &lt;mvpd>sampleMvpdId&lt;/mvpd>
    &lt;requestor>sampleRequestorId&lt;/requestor>
    &lt;resource>sampleResourceId&lt;/resource>
    &lt;/authorization>
    &quot;



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
>當回應來自Proxy MVPD時，可能會包含名為的其他元素 `proxyMvpd`. 

 

* **案例2:拒絕授權**


   ```JSON
   <error>
     <status>403</status>
     <message>User not authorized</message>
     <details>Your subscription package does not include the "ASFAFD" channel.
     Please go to http://www.ca.ble/upgrade in order to upgrade your subscription.</details>
   </error>
   ```
