---
title: 按第二螢幕Web應用檢索預授權資源清單
description: 按第二螢幕Web應用檢索預授權資源清單
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# 按第二螢幕Web應用檢索預授權資源清單 {#retrieve-list-of-preauthorized-resources-by-second-screen-web-app}

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

有兩組API:一組用於流式應用程式或程式設計師服務，另一組用於第二螢幕Web應用程式。 本頁說明AuthN應用程式的API。

 \
|端點 |已呼叫  </br>依據 |輸入   </br>Params | HTTP  </br>方法 |回應 | HTTP  </br>回應 | | — | — | — | — | — | — | | &lt;sp_fqdn>/api/v1/preauthorize/{registration code) | AuthN模組 | 1.  註冊代碼  </br>    （路徑元件）</br>2.  請求者（強制）</br>3.  資源清單（必填） |GET |包含個別預先授權決定或錯誤詳細資訊的XML或JSON。 請參閱以下範例。 | 200 — 成功</br></br>400 — 錯誤請求</br></br>401 — 未授權</br></br>405 — 不允許的方法  </br></br>412 — 先決條件失敗</br></br>500 — 內部伺服器錯誤 |



| 輸入參數 | 說明 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 註冊代碼 | 用戶在驗證流程開始時提供的註冊代碼值。 |
| 請求者 | 此操作對其有效的程式設計師請求者ID。 |
| 資源清單 | 包含resourceIds逗號分隔清單的字串，用於識別使用者可存取且由MVPD授權端點所識別的內容。 |


### 範例回應 {#sample-response}

**XML:**

```XML
HTTP/1.1 200 OK
Adobe-Request-Id : 7af28ec2-a068-45c2-8009-f5443049baf4`
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
    <resource>
</resources>
```

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

