---
title: 檢索預授權資源清單
description: 檢索預授權資源清單
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 檢索預授權資源清單 {#retrieve-list-of-preauthorized-resources}

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

請求Adobe Primetime驗證以取得預先授權資源清單。

有兩組API:一組用於流式應用程式或程式設計師服務，另一組用於第二螢幕Web應用程式。 本頁介紹流應用程式或程式設計師服務的API。


| 端點 | 已呼叫  </br>依據 | 輸入   </br>Params | HTTP  </br>方法 | 回應 | HTTP  </br>回應 |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/preauthorize | 串流應用程式</br></br>或</br></br>程式設計人員服務 | 1.請求者（強制）</br>2.  deviceId（必要）</br>3.  資源清單（必填）</br>4.  device_info/X-Device-Info（強制）</br>5。  _deviceType_</br> 6.  _deviceUser_ （已過時）</br>7.  _appId_ （已過時） | GET | 包含個別預先授權決定或錯誤詳細資訊的XML或JSON。 請參閱以下範例。 | 200 — 成功</br></br>400 — 錯誤請求</br></br>401 — 未授權</br></br>405 — 不允許的方法  </br></br>412 — 先決條件失敗</br></br>500 — 內部伺服器錯誤 |


| 輸入參數 | 說明 |
| --- | --- |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| deviceId | 設備id位元組。 |
| 資源清單 | 包含resourceIds逗號分隔清單的字串，用於識別使用者可存取且由MVPD授權端點所識別的內容。 |
| device_info/</br></br>X-Device-Info | 串流裝置資訊。</br></br>**附註**:此URL可以作為URL參數傳遞，但由於此參數的可能大小及GETURL長度的限制，因此URL應以X-Device-Info在http標題中傳遞。 </br></br><!--See the full details in [Passing Device and Connection Information](http://tve.helpdocsonline.com/passing-device-information)-->. |
| _deviceType_ | 裝置類型（例如Roku、PC）。</br></br>如果此參數設定正確，ESM將提供以下量度： [按設備類型劃分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用無用戶端時，以便執行不同類型的分析，例如Roku、AppleTV和Xbox。</br></br>看， [在傳遞量度中使用無用戶端裝置類型參數的優點&#x200B;](/help/authentication/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)</br></br>**附註**:the `device_info` 會取代此參數。 |
| _deviceUser_ | 裝置使用者識別碼。 |
| _appId_ | 應用程式ID/名稱。 </br></br>**附註**:device_info會取代此參數。 |



### 範例回應 {#sample-response}

 

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/xml; charset=utf-8

<resources>
  <resource>
    <id>TestStream1</id>
    <authorized>true</authorized>
  </resource>
  <resource>
    <id>TestStream2</id>
    <authorized>false</authorized>
    <error>
      <status>403</status>
      <code>authorization_denied_by_mvpd</code>
      <message>User not authorized</message>
      <details>Your subscription package does not include the "TestStream3" channel.</details>
      <helpUrl>https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes</helpUrl>
      <trace>0453f8c8-167a-4429-8784-cd32cfeaee58</trace>
      <action>none</action>
    </error>
  </resource>
</resources>
```
 
</br>

**JSON:**

```JSON
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4
Adobe-Response-Confidence : full
Content-Type: application/json; charset=utf-8
 
{
   "resources" : [
        {
            "id" : "TestStream1",
            "authorized" : true
        },
        {
            "id" : "TestStream3",
            "authorized" : false,
            "error" : {
               "status" : 403,
               "code" : "authorization_denied_by_mvpd",
               "message" : "User not authorized",
               "details" : "Your subscription package does not include the "TestStream3" channel.",
               "helpUrl" : "https://experienceleague-review.corp.adobe.com/docs/primetime/authentication/auth-features/error-reportn/enhanced-error-codes.html#error-codes",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
