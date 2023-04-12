---
title: 動態用戶端註冊API
description: 動態用戶端註冊API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# 動態用戶端註冊API {#dynamic-client-registration-api}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

目前，Primetime驗證有兩種方式可識別和註冊應用程式：

* 瀏覽器型用戶端可透過 [網域清單](/help/authentication/programmer-overview.md)
* 原生應用程式用戶端(例如iOS和Android應用程式)是透過簽署的要求者機制來註冊。

Adobe Primetime身份驗證提出了一種新的應用程式註冊機制。 以下各段對這一機製作了說明。

## 應用程式註冊機制 {#appRegistrationMechanism}

### 技術原因 {#reasons}

Adobe Primetime驗證中的驗證機制原本依賴工作階段Cookie，但原因為 [Android Chrome自訂分頁](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}，這個目標已經無法實現。

基於這些限制，Adobe為所有客戶引進了新的註冊機制。 此範本以OAuth 2.0 RFC為基礎，並包含下列步驟：

1. 從TVE儀表板檢索軟體語句
1. 獲取客戶端憑據
1. 取得存取權杖

### 從TVE儀表板檢索軟體語句 {#softwareStatement}

對於您發佈的每個應用程式，您都需要獲得軟體陳述式。 建立應用程式後，所有軟體語句都通過TVE儀表板提供。 軟體語句應與用戶設備上的應用程式一起部署。

>[!IMPORTANT]
>
>使用軟體陳述式時，不再需要簽名的請求者ID機制。

有關如何建立軟體陳述式的詳細資訊，請訪問 [TVE儀表板中的客戶註冊](/help/authentication/dynamic-client-registration.md).

### 獲取客戶端憑據 {#clientCredentials}

從TVE儀表板檢索軟體語句後，您需要向Adobe Primetime授權伺服器註冊應用程式。 執行/register呼叫並擷取您的唯一用戶端識別碼，即可執行此操作。

**要求**

| HTTP呼叫 |  |
|-----------|--------------------|
| 路徑 | /o/client/register |
| 方法 | POST |

| 欄位 |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | 在TVE儀表板中建立的軟體語句。 | 強制 |
| redirect_uri | 應用程式用於完成身份驗證流的URI。 | 可選 |

| 請求標題 |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| 內容類型 | application/json | 強制 |
| X-Device-Info | 在傳遞設備和連接資訊中定義的設備資訊 | 強制 |
| User-Agent | 使用者代理 | 強制 |

**回應**

| 回應標題 |  |  |
|------------------|------------------|-----------|
| 內容類型 | application/json | 強制 |

| 回應欄位 |  |  |
|---------------------|-----------------|----------------------------|
| client_id | 字串 | 強制 |
| client_secret | 字串 | 強制 |
| client_id_issued_at | long | 強制 |
| redirect_uri | 字串清單 | 強制 |
| grant_types | 字串清單<br/> **接受值**<br/> `client_credentials`:由不安全的用戶端使用，例如Android SDK。 | 強制 |
| 錯誤 | **接受的值**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul> | 錯誤流中的必填項 |


#### 錯誤回應 {#error-response}

如果發生錯誤，註冊伺服器會使用HTTP 400(Bad Request)狀態代碼進行響應，並在響應中包括以下參數：

| 狀態代碼 | 回應體 | 說明 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_request&quot;} | 請求缺少必需的參數、包含不受支援的參數值、重複參數或參數的格式不正確。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_redirect_uri&quot;} | 不允許根據此客戶端的註冊應用程式對其進行redirect_uri。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_software_statement&quot;} | 軟體語句無效。 |
| HTTP 400 | {&quot;error&quot;:&quot;unapproved_software_statement&quot;} | 在配置中找不到software_id。 |

#### 客戶端憑據示例 {#client-credentials-example}

**請求：**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**回應：**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**錯誤回應：**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### 取得存取權杖 {#accessToken}

擷取應用程式的唯一用戶端識別碼（用戶端ID和用戶端密碼）後，您需要取得存取權杖。 存取權杖是強制的OAuth 2.0權杖，用來呼叫Primetime驗證API。

>[!NOTE]
>
>目前，存取權杖的存留時間為24小時。

**要求**


| **HTTP呼叫** |  |
| --- | --- |
| 路徑 | `/o/client/token` |
| 方法 | POST |

| **請求參數** |  |
| --- | --- |
| `grant_type` | 在客戶端註冊過程中接收。<br/> **接受的值**<br/>`client_credentials`:用於不安全的用戶端，例如Android SDK。 |
| `client_id` | 在客戶端註冊過程中獲取的客戶端標識符。 |
| `client_secret` | 在客戶端註冊過程中獲取的客戶端標識符。 |

**回應**

| 回應欄位 |  |  |
| --- | --- | --- |
| `access_token` | 您應用來呼叫Primetime API的存取權杖值 | 強制 |
| `expires_in` | access_token過期的秒數 | 強制 |
| `token_type` | 代號的類型 **承載者** | 強制 |
| `created_at` | 代號的問題時間 | 強制 |
| **回應標題** |  |  |
| `Content-Type` | application/json | 強制 |

**錯誤回應**

如果發生錯誤，授權伺服器會使用HTTP 400(Bad Request)狀態代碼進行回應，並在回應中包含下列參數：

| 狀態代碼 | 回應體 | 說明 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_request&quot;} | 請求缺少必需的參數，包括不受支援的參數值（授權類型除外），重複參數，包括多個憑據，使用多個機制來驗證客戶端，或者其它錯誤。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_client&quot;} | 客戶端身份驗證失敗，因為客戶端未知。 SDK必須重新向授權伺服器註冊。 |
| HTTP 400 | {&quot;error&quot;:&quot;unauthorized_client&quot;} | 已驗證的客戶端無權使用此授權授權類型。 |

#### 取得存取權杖範例： {#obt-access-token}

**請求：**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**回應：**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**錯誤回應：**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## 執行驗證請求 {#autheticationRequests}

使用存取權杖來執行Adobe Primetime [驗證API呼叫](/help/authentication/initiate-authentication.md). 若要這麼做，存取權杖必須透過下列其中一種方式新增至API請求：

* 將新查詢參數新增至請求。 新參數稱為 **access_token**.

* 將新的HTTP標題新增至請求：授權：不記名。 建議您使用HTTP標題，因為查詢字串一般會顯示在伺服器記錄中。

如果發生錯誤，可傳回下列錯誤回應：

| 錯誤回應 |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | 請求的格式不正確。 |
| invalid_client | 403 | 用戶端ID不再允許執行要求。 應生成新的客戶端憑據。 |
| access_denied | 401 | access_token無效（過期或無效）。 用戶端必須要求新的access_token。 |

### 執行驗證請求範例：

**以請求參數傳送存取權杖：**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**以HTTP標題傳送存取權杖：**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**錯誤回應作為回應內文：**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**以URL參數形式回應錯誤：**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
