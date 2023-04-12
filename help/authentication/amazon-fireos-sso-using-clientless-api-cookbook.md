---
title: Amazon FireOS SSO（使用無用戶端API逐步指南）
description: Amazon FireOS SSO（使用無用戶端API逐步指南）
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS SSO（使用無用戶端API逐步指南） {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

## 簡介 {#Introduction}

本檔案提供使用無用戶端API實作Amazon SSO版Adobe Primetime驗證流程的指示。 本檔案的第一部分著重於Amazon版本架構的特定性，因為許多已熟悉且熟悉該架構實施的合作夥伴都有經驗。

檔案的第二部分將介紹實作Adobe Primetime Authentication無用戶端API的主要步驟。

如需無客戶解決方案運作方式的廣泛技術概述，請參閱 [REST API概述](/help/authentication/rest-api-overview.md). Adobe是支援整體架構和首次實作的推薦連絡人。

## Amazon無用戶端SSO {#AMZ-Clientless-SSO}

### 高級體系結構 {#High-Level-Arch}

Amazon無用戶端SSO實作簡單，大多與一般Adobe Primetime驗證無用戶端API相同。

呼叫Adobe無用戶端API時，您需要使用Amazon SDK來擷取個人化裝載，並使用它。

如果已識別裝載且與已驗證的工作階段對應，無用戶端API將會立即以您工作階段的Token傳回。

### 如何建置應用程式以使用Amazon SDK {#Build-entries}

* 下載並複製最新 [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) 並行到應用目錄的/SSOEnabler資料夾
* 更新資訊清單/Gradle檔案以使用程式庫：

   **將下列行新增至您的資訊清單檔案：**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Gradle檔案項：**

   在儲存庫下：

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   在相依性下，新增：

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* 處理缺少Amazon隨附應用程式的問題：

   雖然不太可能，但如果您的應用程式正在運行的Amazon設備上不存在該配對，您應該在以下類的運行時遇到ClassNotFoundException: `com.amazon.ottssotokenlib.SSOEnabler`.

   如果發生此情況，您只需略過裝載步驟，然後回復到一般的PrimeTime流程即可。 不會啟用SSO，但正常驗證流程會正常進行。

</br>

### 如何使用Amazon SDK取得Amazon SSO裝載 {#UseAmazonSSO}

在應用程式初始化期間，獲取SSOEnabler實例。 您應根據您的應用程式架構，決定是同步還是非同步實作。

如果因任何原因，API呼叫不會傳回裝載，請使用一般的非SSO流程，並連絡您的Amazon和Adobe合作夥伴進行調查。

**非同步API**

* 獲取SSO啟用程式實例：

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* 設定回呼 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * 成功回應套件組合將包含：
      * SSO代號，作為鍵為&quot;SSOToken&quot;的字串
   * 失敗響應包將包含：
      * 以int形式使用鍵「ErrorCode」的錯誤代碼
      * 錯誤描述為鍵為&quot;ErrorDescription&quot;的字串


* 取得SSO代號

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 此API會在初始化期間透過回呼設定提供回應。

   **Ex**. 使用在init期間建立的單例實例調用：

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**同步API**

* 獲取SSO啟用程式實例並設定回調

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* 取得SSO代號

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 此API將阻止呼叫者線程，並以結果包進行響應。 由於這是同步呼叫，請務必勿在主執行緒中使用它。

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 值（以毫秒為單位）。 若已設定，請覆寫同步API的預設逾時值1分鐘。



### Adobe Primetime無用戶端API更新以使用Dynamic Client Registration {#clientlessdcr}

如果這是您的第一個實作，請參閱 **無客戶端技術概述** 並聯絡Adobe以備您需要支援時使用。

Adobe無用戶端API要求應用程式使用動態客戶端註冊，以便對Adobe伺服器進行呼叫。

* 若要在您的應用程式中使用動態用戶端註冊，請遵循 [ Dynamic Client Registration Management以註冊應用程式](/help/authentication/dynamic-client-registration-management.md).

* 若要實作Dynamic Client Registration API以對Adobe Primetime伺服器執行驗證和授權要求，請遵循 [動態用戶端註冊API](/help/authentication/dynamic-client-registration-api.md) .

### Adobe Primetime無用戶端API更新以使用Amazon SSO {#clientlesssso}

從Amazon SDK取得的Amazon SSO裝載必須存在於向Adobe Primetime驗證端點提出的請求中：

```
      /adobe-services/*
      /reggie/*
      /api/*
```


所有Primetime驗證端點都支援下列方法，以接收裝置範圍識別碼或平台範圍識別碼(出現在Amazon SSO裝載中):

* 作為標題：&quot;Adobe — 主體 — 代號&quot;
* 作為查詢參數：&quot;ast&quot;
* 作為貼文參數：&quot;ast&quot;


>[!NOTE]
>
>如果裝置範圍識別碼或平台範圍識別碼是以查詢/貼文參數的形式傳送，則在產生請求籤章時必須包含它。

>[!NOTE]
>
>使用查詢參數「ast」時，整個URL可能會變長且遭拒。 在/authenticate呼叫上，此參數可如/regcode呼叫所提供，而予以略過

**範例：**

**以自訂標頭傳送**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**傳送作為查詢參數**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**以貼文參數傳送**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>如果Amazon SSO不存在或無效，Adobe Primetime驗證將忽略屬性，並且會如同SSO不存在一樣執行呼叫。
