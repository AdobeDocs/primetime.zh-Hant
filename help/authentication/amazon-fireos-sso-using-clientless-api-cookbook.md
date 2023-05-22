---
title: AmazonFireOS SSO使用無客戶端API指南
description: AmazonFireOS SSO使用無客戶端API指南
exl-id: 4c65eae7-81c1-4926-9202-a36fd13af6ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# AmazonFireOS SSO使用無客戶端API指南 {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

## 導言 {#Introduction}

本文檔提供了使用無客戶端API實現AmazonSSO版本的Adobe Primetime身份驗證流的說明。 本檔案的第一部分側重於Amazon版本的體系結構的具體性，對於許多已經熟悉和經驗豐富的合作夥伴來說。

文檔的第二部分介紹了實現Adobe Primetime驗證無客戶端API的主要步驟。

有關無客戶端解決方案工作原理的全面技術概述，請參見 [REST API概述](/help/authentication/rest-api-overview.md)。 Adobe是支援整體體系結構和第一個實施的首選聯繫人。

## Amazon無客戶端SSO {#AMZ-Clientless-SSO}

### 高級體系結構 {#High-Level-Arch}

Amazon無客戶端SSO實現簡單，與常規的Adobe Primetime無客戶端API基本相同。

您需要使用AmazonSDK檢索個性化負載，並在調用Adobe無客戶端API時使用它。

如果負載被識別並且與經過驗證的會話相對應，則無客戶端API將立即返回，並返回您的會話的令牌。

### 如何構建應用程式以使用AmazonSDK {#Build-entries}

* 下載並複製最新 [Amazon小作品SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) 到與app目錄平行的/SSOEnabler資料夾
* 更新清單/格式檔案以使用庫：

   **將以下行添加到清單檔案：**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **梯度檔案條目：**

   在儲存庫下：

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   在依賴項下，添加：

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* 處理Amazon配套應用的缺失：

   雖然不太可能，但是如果您的應用程式正在運行的Amazon設備上沒有該陪同程式，您應該在以下類的運行時遇到ClassNotFoundException: `com.amazon.ottssotokenlib.SSOEnabler`。

   如果發生這種情況，您只需跳過負載步驟並返回常規PrimeTime流。 將不啟用SSO，但常規身份驗證流將正常進行。

</br>

### 如何使用AmazonSDK獲取AmazonSSO負載 {#UseAmazonSSO}

在應用程式初始化期間，獲取SSOEnabler的實例。 您應根據您的應用程式體系結構，在同步或非同步實施之間做出選擇。

如果由於任何原因，API調用不返回負載，請使用常規的非SSO流，並與您的Amazon和Adobe合作夥伴聯繫以進行調查。

**非同步API**

* 獲取SSO Enabler實例：

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* 設定回調 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * 成功響應包將包含：
      * SSO令牌，作為鍵為&quot;SSOToken&quot;的字串
   * 失敗響應包將包含：
      * 錯誤代碼，作為鍵為&quot;ErrorCode&quot;的int
      * 錯誤描述，以鍵「ErrorDescription」的字串形式表示


* 獲取SSO令牌

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 此API將在初始化期間通過回調集提供響應。

   **前**。 使用在init期間建立的singleton實例調用：

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**同步API**

* 獲取SSO Enabler實例並設定回調

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* 獲取SSO令牌

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 此API將阻止調用方線程，並以結果包響應。 由於這是同步呼叫，請確保不要在主線程中使用它。

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 值（毫秒）。 如果設定，則覆蓋同步API的預設超時值1分鐘。



### Adobe Primetime無客戶端API更新以使用動態客戶端註冊 {#clientlessdcr}

如果這是您的第一個實施，請參閱 **無客戶端技術概述** 和聯繫Adobe，以備您需要支援。

Adobe無客戶端API要求應用程式使用動態客戶端註冊，以便調用Adobe伺服器。

* 要在應用程式中使用動態客戶端註冊，請按照中的說明 [ 動態客戶端註冊管理以註冊應用程式](/help/authentication/dynamic-client-registration-management.md)。

* 要實施動態客戶端註冊API以執行對Adobe Primetime伺服器的身份驗證和授權請求，請按照中的說明操作 [動態客戶端註冊API](/help/authentication/dynamic-client-registration-api.md) 。

### Adobe Primetime無客戶端API更新以使用AmazonSSO {#clientlesssso}

從AmazonSDK獲取的AmazonSSO負載需要在向Adobe Primetime身份驗證端點發出的請求中顯示：

```
      /adobe-services/*
      /reggie/*
      /api/*
```


所有黃金時段身份驗證終結點都支援以下方法來接收設備範圍標識符或平台範圍標識符(在AmazonSSO負載中存在):

* 作為標頭：&quot;Adobe主題標籤&quot;
* 作為查詢參數：&quot;ast&quot;
* 作為帖子參數：&quot;ast&quot;


>[!NOTE]
>
>如果將設備範圍標識符或平台範圍標識符作為查詢/帖子參數發送，則在生成請求籤名時必須包括它。

>[!NOTE]
>
>使用查詢參數「ast」，整個URL可能會變得非常長並被拒絕。 在/authenticate調用中，可跳過此參數，因為它在/regcode調用中提供了該參數

**示例：**

**作為自定義標頭髮送**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**作為查詢參數發送**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**正在作為帖子參數發送**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>如果AmazonSSO不存在或無效，Adobe Primetime身份驗證將忽略該屬性，並且將執行調用，就好像SSO不存在一樣。
