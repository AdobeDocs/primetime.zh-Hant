---
title: 按第二螢幕Web應用檢索預授權資源清單
description: 按第二螢幕Web應用檢索預授權資源清單
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 按第二螢幕Web應用檢索預授權資源清單 {#retrieve-list-of-preauthorized-resources-by-second-screen-web-app}

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

請求Adobe Primetime驗證以獲取預授權資源清單。

有兩組API:一組用於流式應用程式或程式設計師服務，另一組用於第二螢幕Web應用。 此頁描述AuthN應用的API。

 \
|端點 |調用  </br>按 |輸入   </br>帕拉姆 | HTTP  </br>方法 |響應 | HTTP  </br>響應 | | - | - | - | - | - | - | | &lt;sp_fqdn>/api/v1/preauthorize/{註冊代碼 | AuthN模組 | 1。  註冊碼  </br>    （路徑元件）</br>2.  請求者（必需）</br>3.  資源清單（必需） |GET | XML或JSON包含單個預授權決定或錯誤詳細資訊。 請參見下面的示例。 | 200 — 成功</br></br>400 — 錯誤請求</br></br>401 — 未授權</br></br>405 — 不允許使用方法  </br></br>412 — 先決條件失敗</br></br>500 — 內部伺服器錯誤 |



| 輸入參數 | 說明 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 註冊碼 | 用戶在驗證流開始時提供的註冊代碼值。 |
| 請求 | 此操作對其有效的程式設計師請求者ID。 |
| 資源清單 | 包含以逗號分隔的resourceId清單的字串，該清單標識用戶可訪問且由MVPD授權端點識別的內容。 |


### 示例響應 {#sample-response}

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
            <helpUrl>https://tve.helpdocsonline.com/errors/preauthorization_denied</helpUrl>
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
               "helpUrl" : "https://tve.helpdocsonline.com/errors/preauthorization_denied",
               "trace" : "0453f8c8-167a-4429-8784-cd32cfeaee58",
               "action" : "none"
            }
        } 
    ]
}
```
 

### [返回REST API參考](http://tve.helpdocsonline.com/rest-api-reference)
