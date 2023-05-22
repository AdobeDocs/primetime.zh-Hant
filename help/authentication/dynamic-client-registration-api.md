---
title: 動態客戶端註冊API
description: 動態客戶端註冊API
exl-id: 06a76c71-bb19-4115-84bc-3d86ebcb60f3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 動態客戶端註冊API {#dynamic-client-registration-api}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

目前，Mogine Authentication可通過兩種方式識別和註冊應用程式：

* 允許註冊基於瀏覽器的客戶端 [域清單](/help/authentication/programmer-overview.md)
* 本地應用程式客戶端(如iOS和Android應用程式)通過簽名請求者機制註冊。

Adobe Primetime認證提出了一種新的註冊機制。 這一機制在以下各段中作了說明。

## 申請登記機制 {#appRegistrationMechanism}

### 技術原因 {#reasons}

Adobe Primetime身份驗證中的身份驗證機制依賴會話cookie，但是 [Android Chrome自定義頁籤](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}這個目標已經不能再實現了。

鑒於這些限制，Adobe為其所有客戶引入了新的註冊機制。 它基於OAuth 2.0 RFC，並包括以下步驟：

1. 從TVE儀表板檢索軟體語句
1. 獲取客戶端憑據
1. 獲取訪問令牌

### 從TVE儀表板檢索軟體語句 {#softwareStatement}

對於您發佈的每個應用程式，您都需要獲得軟體語句。 建立應用程式後，所有軟體語句都通過TVE Dashboard提供。 軟體語句應與用戶設備上的應用程式一起部署。

>[!IMPORTANT]
>
>使用軟體語句時，不再需要簽名的請求者ID機制。

有關如何建立軟體語句的詳細資訊，請訪問 [TVE儀表板中的客戶端註冊](/help/authentication/dynamic-client-registration.md)。

### 獲取客戶端憑據 {#clientCredentials}

從TVE Dashboard中檢索軟體語句後，您需要向Adobe Primetime授權伺服器註冊您的應用程式。 通過執行/register調用並檢索您的唯一客戶端標識符來執行此操作。

**請求**

| HTTP調用 |  |
|-----------|--------------------|
| 路徑 | /o/client/register |
| 方法 | POST |

| 欄位 |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| 軟體_語句 | 在TVE儀表板中建立的軟體語句。 | 強制 |
| 重定向/uri | 應用程式用於完成驗證流的URI。 | 可選 |

| 請求標題 |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| 內容類型 | 應用程式/json | 強制 |
| X設備資訊 | 在傳遞設備和連接資訊中定義的設備資訊 | 強制 |
| 用戶代理 | 用戶代理 | 強制 |

**響應**

| 響應標題 |  |  |
|------------------|------------------|-----------|
| 內容類型 | 應用程式/json | 強制 |

| 響應欄位 |  |  |
|---------------------|-----------------|----------------------------|
| 客戶端ID | 字串 | 強制 |
| 客戶端密鑰 | 字串 | 強制 |
| 客戶端_id_issiqued_at | 長 | 強制 |
| 重定向_uris | 字串清單 | 強制 |
| grant_types | 字串清單<br/> **接受值**<br/> `client_credentials`:由不安全的客戶端（如Android SDK）使用。 | 強制 |
| 錯誤 | **接受值**<ul><li>無效請求</li><li>無效_redirect_uri</li><li>無效_software_statement</li><li>unapproved_software_statement</li></ul> | 錯誤流中的必需項 |


#### 錯誤響應 {#error-response}

如果出現錯誤，註冊伺服器用HTTP 400（錯誤請求）狀態代碼響應，並在響應中包括以下參數：

| 狀態代碼 | 反應體 | 描述 |
| --- | --- | --- |
| HTTP 400 | {「error」（錯誤）:&quot;無效_請求&quot; | 請求缺少必需的參數、包含不受支援的參數值、重複參數或其格式不正確。 |
| HTTP 400 | {「error」（錯誤）:&quot;無效_redirect_uri&quot; | 基於此客戶端註冊的應用程式，不允許使用redirect_uri。 |
| HTTP 400 | {「error」（錯誤）:&quot;無效_software_statement&quot;} | 軟體語句無效。 |
| HTTP 400 | {「error」（錯誤）:&quot;未批准_軟體_語句&quot;} | 在配置中找不到software_id。 |

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

**響應：**

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

**錯誤響應：**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### 獲取訪問令牌 {#accessToken}

在為您的應用程式檢索唯一客戶端標識符（客戶端ID和客戶端機密）後，您需要獲取訪問令牌。 訪問令牌是強制OAuth 2.0令牌，用於調用黃金時段驗證API。

>[!NOTE]
>
>目前，訪問令牌有24小時的生存時間。

**請求**


| **HTTP調用** |  |
| --- | --- |
| 路徑 | `/o/client/token` |
| 方法 | POST |

| **請求參數** |  |
| --- | --- |
| `grant_type` | 在客戶端註冊過程中接收。<br/> **接受值**<br/>`client_credentials`:用於不安全的客戶端，如Android SDK。 |
| `client_id` | 在客戶端註冊過程中獲取的客戶端標識符。 |
| `client_secret` | 在客戶端註冊過程中獲取的客戶端標識符。 |

**響應**

| 響應欄位 |  |  |
| --- | --- | --- |
| `access_token` | 您應用於調用黃金時段API的訪問令牌值 | 強制 |
| `expires_in` | access_token過期前的時間（秒） | 強制 |
| `token_type` | 令牌的類型 **載體** | 強制 |
| `created_at` | 令牌的發佈時間 | 強制 |
| **響應標題** |  |  |
| `Content-Type` | 應用程式/json | 強制 |

**錯誤響應**

如果出現錯誤，授權伺服器用HTTP 400（錯誤請求）狀態代碼響應，並在響應中包括以下參數：

| 狀態代碼 | 反應體 | 描述 |
| --- | --- | --- |
| HTTP 400 | {「error」（錯誤）:&quot;無效_請求&quot; | 該請求缺少所需參數、包括不受支援的參數值（除授予類型外）、重複參數、包括多個憑據、使用多個機制來驗證客戶端，或者格式不正確。 |
| HTTP 400 | {「error」（錯誤）:&quot;無效_客戶端&quot;} | 客戶端身份驗證失敗，因為客戶端未知。 SDK必須再次向授權伺服器註冊。 |
| HTTP 400 | {「error」（錯誤）:&quot;未授權客戶端&quot;} | 已驗證的客戶端無權使用此授權授權類型。 |

#### 獲取訪問令牌示例： {#obt-access-token}

**請求：**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**響應：**

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

**錯誤響應：**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## 執行身份驗證請求 {#autheticationRequests}

使用訪問令牌執行Adobe Primetime [驗證API調用](/help/authentication/initiate-authentication.md)。 為此，需要通過以下方法之一將訪問令牌添加到API請求中：

* 通過向請求添加新查詢參數。 該新參數稱為 **訪問令牌**。

* 通過向請求添加新HTTP標頭：授權：持牌人。 建議您使用HTTP標頭，因為查詢字串在伺服器日誌中往往可見。

如果出現錯誤，可返回以下錯誤響應：

| 錯誤響應 |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| 無效請求 | 400 | 請求格式不正確。 |
| 無效的客戶端 | 403 | 不再允許客戶端ID執行請求。 應生成新的客戶端憑據。 |
| 拒絕訪問 | 401 | access_token無效（已過期或無效）。 客戶端必須請求新的access_token。 |

### 執行身份驗證請求示例：

**將訪問令牌作為請求參數發送：**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**將訪問令牌作為HTTP標頭髮送：**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**錯誤響應作為響應主體：**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**響應為URL參數時出錯：**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
