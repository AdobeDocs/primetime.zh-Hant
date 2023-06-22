---
title: 使用無使用者端API逐步指南的Amazon FireOS SSO
description: 使用無使用者端API逐步指南的Amazon FireOS SSO
exl-id: 4c65eae7-81c1-4926-9202-a36fd13af6ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 使用無使用者端API逐步指南的Amazon FireOS SSO {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

</br>

## 簡介 {#Introduction}

本檔案提供使用無使用者端API實作Amazon SSO版Adobe Primetime驗證流程的說明。 本檔案的第一部分著重於架構的Amazon版本特性，適合許多熟悉並熟悉其實作的合作夥伴使用。

本檔案的第二部分說明實作Adobe Primetime驗證無使用者端API的主要步驟。

如需無使用者端解決方案運作方式的廣泛技術概覽，請參閱 [REST API概觀](/help/authentication/rest-api-overview.md). Adobe是取得整體架構和第一個實作相關支援的偏好連絡方式。

## Amazon無使用者端SSO {#AMZ-Clientless-SSO}

### 高階架構 {#High-Level-Arch}

Amazon無使用者端SSO實作相當簡單，且大多與一般Adobe Primetime驗證無使用者端API相同。

您將需要使用Amazon SDK來擷取個人化裝載，並在呼叫Adobe無使用者端API時使用。

如果可辨識裝載且對應至已驗證的工作階段，則無使用者端API會立即傳回工作階段的Token。

### 如何建置應用程式以使用Amazon SDK {#Build-entries}

* 下載並複製最新版 [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) 併入/SSOEnabler資料夾，與app目錄平行
* 更新資訊清單/Gradle檔案以使用程式庫：

   **將下列行新增至資訊清單檔案：**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Gradle檔案專案：**

   在存放庫下：

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   在相依性下方，新增：

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* 處理缺少Amazon隨附應用程式的情況：

   雖然不太可能，但如果您的應用程式正在執行的Amazon裝置上沒有隨附，您應該會在下列類別的執行階段遇到ClassNotFoundException： `com.amazon.ottssotokenlib.SSOEnabler`.

   如果發生此情況，您只需要略過裝載步驟，然後回覆一般PrimeTime流程即可。 將不會啟用SSO，但正常會發生一般驗證流程。

</br>

### 如何使用Amazon SDK取得Amazon SSO裝載 {#UseAmazonSSO}

在您的應用程式初始化期間，取得SSOEnabler的執行個體。 根據您的應用程式架構，您應決定是同步實施還是非同步實施。

如果由於任何原因，API呼叫沒有傳回裝載，請使用正常的非SSO流程，並聯絡您的Amazon和Adobe合作夥伴以調查。

**非同步API**

* 取得SSO啟用程式執行個體：

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* 設定回撥 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * 成功回應套件組合將包含：
      * SSO權杖為具有索引鍵「SSOToken」的字串
   * 失敗回應套件組合將包含：
      * 錯誤碼為int，並附上索引鍵「ErrorCode」
      * 錯誤說明（含索引鍵「ErrorDescription」的字串）


* 取得SSO權杖

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 此API將透過初始期間設定的回呼提供回應。

   **例如**. 使用在初始化期間建立的單一例項呼叫：

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**同步API**

* 取得SSO Enabler執行個體並設定回呼

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* 取得SSO權杖

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 此API將封鎖呼叫者對話串，並以結果套件回應。 由於這是同步呼叫，請勿在主執行緒上使用。

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 值（以毫秒為單位）。 如果設定，會覆寫同步API的預設逾時值1分鐘。



### Adobe Primetime無使用者端API更新以使用動態使用者端註冊 {#clientlessdcr}

如果這是您的首次實作，請參閱 **無使用者端技術概覽** 並聯絡Adobe以備您需要支援時使用。

Adobe無使用者端API要求應用程式使用動態使用者端註冊，以便呼叫Adobe伺服器。

* 若要在應用程式中使用Dynamic Client Registration，請依照下列指示操作： [ Dynamic Client Registration Management註冊應用程式](/help/authentication/dynamic-client-registration-management.md).

* 若要實作動態使用者端註冊API以對Adobe Primetime伺服器執行驗證和授權請求，請依照以下說明操作： [動態使用者端註冊API](/help/authentication/dynamic-client-registration-api.md) .

### Adobe Primetime無使用者端API更新以使用Amazon SSO {#clientlesssso}

向Amazon驗證端點提出的請求中，必須存在從Amazon SDK取得的Adobe Primetime SSO裝載：

```
      /adobe-services/*
      /reggie/*
      /api/*
```


所有Primetime驗證端點都支援下列方法來接收裝置範圍識別碼或平台範圍識別碼(出現在Amazon SSO裝載中)：

* 作為標頭：&quot;Adobe-Subject-Token&quot;
* 作為查詢引數：&quot;ast&quot;
* 作為貼文引數：&quot;ast&quot;


>[!NOTE]
>
>如果裝置範圍識別碼或平台範圍識別碼是以查詢/張貼引數的形式傳送，則產生請求籤章時必須包含此識別碼。

>[!NOTE]
>
>使用查詢引數&quot;ast&quot;，整個URL可能會變得非常長並被拒絕。 在/authenticate呼叫上，可以略過此引數，因為它是在/regcode呼叫上提供的

**範例：**

**以自訂標題傳送**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**以查詢引數傳送**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**以張貼引數傳送**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>如果Amazon SSO不存在或無效，Adobe Primetime驗證將會忽略屬性，並像SSO不存在一樣執行呼叫。
