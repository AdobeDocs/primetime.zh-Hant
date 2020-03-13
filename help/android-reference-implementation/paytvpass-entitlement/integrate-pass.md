---
description: 自訂您的參考實作，以整合Adobe Primetime驗證以用於您的生產環境。
seo-description: 自訂您的參考實作，以整合Adobe Primetime驗證以用於您的生產環境。
seo-title: 整合Primetime驗證
title: 整合Primetime驗證
uuid: 34cdf1da-261e-462c-a194-4fcb439e5dfb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 整合Primetime驗證 {#integrate-primetime-authentication}

自訂您的參考實作，以整合Adobe Primetime驗證以用於您的生產環境。

Primetime驗證服務的「參考實作」整合現成可用的展示。 不過，若要在生產就緒播放器中使用整合，您必須實作下列自訂設定：

1. 啟用或停用權益流程。

   必須先 `EntitlementManager` 初始化並取得要啟用的Primetime驗證SDK例項。 如果未 `EntitlementManager` 初始化此庫，則將禁用管理器。
1. 從您的 `EntitlementManger`主應用程式類中啟用：

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 使用 `ManagerFactory` 類獲取實例 `EntitlementManager`。

   您必須始終使用 `ManagerFactory` 來取得的例項，因 `EntitlementManager`為應 `ManagerFactory` 用程式會維護單一的EntitlementManager例項。 切勿使用其 `EntitlementManager` 建構子 `EntitlementManagerOn` 實例化或類。

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   如 `ManagerFactory` 果您先前呼叫 `EntitlementManagerOn`過，則會傳回例項，並啟用權益流程 `EntitlementManager.initializeAccessEnabler`。 如果您未先呼叫 `EntitlementManager.initializeAccessEnabler`，則會傳 `ManagerFactory` 回例項 `EntitlementManager`，且權益流程已停用。 1.設定請求者ID。

   參考實作已預先設定，測試請求者ID設定為：&quot;REF&quot;。 您可以使用此請求者ID來測試您的應用程式。 當您準備好使用Primetime驗證代表提供給您的請求者ID時，請使用您的請求者ID更新應 [!DNL res/values/strings.xml] 用程式的檔案。

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

   此外，您可能需要變更您的應用程式用來連線至Primetime驗證服務的URL。 這些包括Primetime驗證接移和生產伺服器URL，以及Token驗證服務的URL。 請洽詢您的Adobe Primetime代表以取得詳細資訊。 1.簽署申請人ID。

   為了在Primetime認證系統中建立節目編排者的身份，節目編排者請求者ID被發送到Primetime認證系統。 作為新增的安全層，要求者ID必須先由程式設計人員簽署，才能將它傳送至Adobe。 Adobe建議程式設計人員在受信任的網路上設定服務，以簽署要求者ID。

   Primetime參考實作示範如何簽署請求者ID，但僅供展示之用。 Adobe強烈建議，簽署憑證和簽名產生器程式碼(位 `com.adobe.primetime.reference.crypto`於下方)不應包含在生產應用程式中。 相反，您應將其移至值得信賴的網路服務。

1. 配置伺服器環境。

   Primetime驗證服務可在兩個不同的環境中執行：

   * 測試——測試環境用於測試您的應用程式。
   * 生產——生產環境用於即時部署您的應用程式。
   您使用應用程式為測試環境和生產環境設定URI，但您必須設定程式碼中的應用程式所使用的URI。 在類 `com.adobe.primetime.reference.manager.EntitlementManger` 別中，將變數設 `environmentUri` 定為 `STAGING_URI` 或視您使用的 `PRODUCTION_URI` Primetime驗證服務環境而定。

   >[!NOTE]
   >
   >提供的請求者ID(「REF」)僅應與測試環境一起使用。

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

1. 自訂MVPD選取格線。

   內容提供者選擇頁面會顯示使用者可從中選取的前9個MVPD的表格。 應用程式會從應用程式內的順序清單中提取前9個MVPD，這些順序清單會符合與Primetime驗證系統中程式設計人員整合的可用MVPD。 主要MVPD的順序清單會在Primetime驗證系統的MVPD ID上輸入，而非MVPD顯示名稱。 請務必確認主要MVPD清單中的MVPD ID與與程式設計人員帳戶整合的MVPD ID相符，因為在某些情況下，ID在整合時可能不同。 以下是類中找到的主MVPD的有序清單 `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`。

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

   下表提供如何使用主要MVPD的有序清單的範例。 第一欄會列出與程式設計人員整合的MVPD。 第二欄是MVPD的（縮短）順序清單。 第三欄是用來向使用者顯示前6個MVPD的結果清單。

   此範例使用前6個MVPD，而非實際的9個MVPD，讓範例保持簡單。 請注意，結果清單如何包含前兩個清單的交叉點，並具有與第二個清單相同的順序。 此外，請注意，AT&amp;T U-verse不在最終清單中，因為只會取得第一個符合的6個MVPD。

| 可用的MVPD | 主要MVPD | 顯示6個MVPD |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>碟</li><li>AT&amp;T U-verse</li><li>CableOne</li><li>光明屋</li><li>Atlantic Broadband</li><li>哇！</li><li>MetroCast</li><li>DirectTV </li><li>考克斯</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟</li><li> TWC</li><li>考克斯</li><li>憲章</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T U-verse</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟</li><li>TWC</li><li>考克斯</li><li>Cablevision Optimum</li></ol> |
