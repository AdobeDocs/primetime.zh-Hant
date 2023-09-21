---
description: 自訂您的參考實作，為您的生產環境整合Adobe Primetime驗證。
title: 整合Primetime驗證
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 整合Primetime驗證 {#integrate-primetime-authentication}

自訂您的參考實作，為您的生產環境整合Adobe Primetime驗證。

Primetime驗證服務的參考實作整合可立即用於示範。 不過，若要在生產就緒播放器中使用整合，您必須實作下列自訂：

1. 啟用或停用權益流程。

   此 `EntitlementManager` 必須先初始化並取得要啟用的Primetime驗證SDK執行個體。 如果 `EntitlementManager` 不會初始化此程式庫，管理員將會停用。
1. 啟用 `EntitlementManger`，從您的主要應用程式類別：

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 使用 `ManagerFactory` 類別以取得 `EntitlementManager`.

   您必須一律使用 `ManagerFactory` 若要取得 `EntitlementManager`，作為 `ManagerFactory` 維護應用程式的單一EntitlementManager執行個體。 永遠不要例項化 `EntitlementManager` 或 `EntitlementManagerOn` 類別使用它們的建構函式。

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   此 `ManagerFactory` 傳回例項 `EntitlementManagerOn`，並啟用權益流程(如果您先前呼叫 `EntitlementManager.initializeAccessEnabler`. 如果您沒有先呼叫 `EntitlementManager.initializeAccessEnabler`，然後 `ManagerFactory` 將傳回的例項 `EntitlementManager`，並停用權益流程。 1.設定請求者ID。

   此參考實作會預先設定測試請求者ID設為：&quot;REF&quot;。 您可以使用此要求者ID來測試您的應用程式。 當您準備好使用Primetime驗證代表提供給您的請求者ID時，請更新應用程式的 [!DNL res/values/strings.xml] 具有您的請求者ID的檔案。

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   此外，您可能需要變更應用程式用來連線至Primetime驗證服務的URL。 其中包括Primetime驗證測試和生產伺服器URL，以及權杖驗證服務的URL。 請洽詢您的Adobe Primetime代表以取得詳細資訊。 1.簽署請求者ID。

   為了在Primetime驗證系統中建立程式設計師的身分，程式設計師的請求者ID會傳送到Primetime驗證系統。 作為新增的安全性層，要求者ID必須先由程式設計師簽署，才能傳送給Adobe。 Adobe建議程式設計師設定服務，在信任的網路上簽署要求者ID。

   Primetime參考實作會示範如何簽署請求者ID，不過此僅供示範之用。 Adobe強烈建議簽署憑證和簽章產生器程式碼位於 `com.adobe.primetime.reference.crypto`、不應納入生產應用程式。 相反地，您應該將它移至信任的網路服務。

1. 設定伺服器環境。

   Primetime驗證服務可以在兩個不同的環境中執行：

   * 測試 — 測試環境用於測試您的應用程式。
   * 生產 — 生產環境用於應用程式的即時部署。

   您可使用應用程式為中繼和生產環境設定URI，但您必須在程式碼中設定應用程式使用哪一個URI。 在 `com.adobe.primetime.reference.manager.EntitlementManger` 類別，設定 `environmentUri` 變數至 `STAGING_URI` 或 `PRODUCTION_URI` 視您使用的Primetime驗證服務環境而定。

   >[!NOTE]
   >
   >提供的要求者ID (「REF」)應僅用於中繼環境。

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. 自訂MVPD選取方格。

   「內容提供者選擇」頁面會顯示一個表格，列出使用者可選擇的前九個MVPD。 應用程式會從應用程式內的已排序清單中提取前九個MVPD，這些清單與Primetime驗證系統中與程式設計師整合的可用MVPD相符。 主要MVPD的排序清單是以Primetime驗證系統內的MVPD ID作為索引鍵，而非MVPD顯示名稱。 務必確認主要MVPD清單中的MVPD ID符合與程式設計師帳戶整合的MVPD ID，因為在某些情況下，整合中的ID可能會不同。 以下是在類別中找到的主要MVPD的排序清單 `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   下表提供如何使用主要MVPD的排序清單的範例。 第一欄列出與程式設計師整合的MVPD。 第二欄是MVPD的（縮短）排序清單。 第三欄是用來向使用者顯示前六個MVPD的結果清單。

   此範例使用前六個MVPD，而非實際的9個，以簡化範例。 請注意結果清單如何包含前兩個清單的交集，且排序與第二個清單相同。 此外，請注意，AT&amp;T U版本不在最終清單中，因為只擷取第一個相符的6個MVPD。

| 可用的MVPD | 主要MVPD | 顯示6個MVPD |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>碟子</li><li>AT&amp;T反向</li><li>纜線One</li><li>Brighthouse</li><li>大西洋寬頻</li><li>哇！</li><li>Metrocast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟子</li><li> TWC</li><li>Cox</li><li>憲章</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T反向</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟子</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol> |
