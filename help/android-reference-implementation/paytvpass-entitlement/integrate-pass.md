---
description: 自定義您的參考實施，為您的生產環境整合Adobe Primetime身份驗證。
title: 整合Mighine身份驗證
exl-id: ef6dc75d-d00f-481f-a620-4ec402cbebb6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 整合Mighine身份驗證 {#integrate-primetime-authentication}

自定義您的參考實施，為您的生產環境整合Adobe Primetime身份驗證。

黃金時段認證服務的參考實施整合以現成方式進行演示。 但是，要在生產就緒型播放器中使用整合，必須實現以下自定義：

1. 啟用或禁用權利流。

   的 `EntitlementManager` 必須首先初始化並獲取要啟用的Mogifle身份驗證SDK的實例。 如果 `EntitlementManager` 不初始化此庫，將禁用管理器。
1. 啟用 `EntitlementManger`，從主應用程式類中：

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 使用 `ManagerFactory` 類以獲取實例 `EntitlementManager`。

   您必須始終使用 `ManagerFactory` 來獲取一個 `EntitlementManager`，也請參見Wiki頁。 `ManagerFactory` 為您的應用程式維護EntitlementManager的單個實例。 從不實例化 `EntitlementManager` 或 `EntitlementManagerOn` 類。

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   的 `ManagerFactory` 返回的實例 `EntitlementManagerOn`，如果您以前調用了權利流，則啟用權利流 `EntitlementManager.initializeAccessEnabler`。 如果你不先打電話 `EntitlementManager.initializeAccessEnabler`，則 `ManagerFactory` 將返回的實例 `EntitlementManager`，並禁用權利流。 1。配置請求者ID。

   參考實現預配置了test請求者ID，設定為：&quot;REF&quot;。 您可以使用此請求者ID來test應用程式。 當您準備好使用黃金時段驗證代表提供給您的請求者ID時，請更新應用程式 [!DNL res/values/strings.xml] 檔案和請求者ID。

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

   此外，您可能需要更改您的應用程式用於連接到黃金時段身份驗證服務的URL。 這些包括黃金時段驗證登台和生產伺服器URL以及令牌驗證服務的URL。 請咨詢您的Adobe Primetime代表，瞭解詳情。 1。簽署請求者ID。

   為了在黃金時段認證系統內建立程式設計師的身份，程式設計師的請求者ID被發送到黃金時段認證系統。 作為增加的安全層，在將請求者ID發送到Adobe之前，必須由程式設計師簽名。 Adobe建議程式設計師設定服務，以在受信任的網路上簽名請求者ID。

   黃金時段參考實現演示了如何簽署請求者ID，但這僅用於演示目的。 Adobe強烈建議簽名證書和簽名生成器代碼 `com.adobe.primetime.reference.crypto`，不應包含在生產應用程式中。 相反，您應將其移動到受信任的網路服務。

1. 配置伺服器環境。

   黃金時段身份驗證服務可以在兩個不同的環境中運行：

   * 轉移 — 轉移環境用於測試您的應用程式。
   * 生產 — 生產環境用於應用程式的即時部署。

   您使用應用程式為登台環境和生產環境設定了URI，但必須設定代碼中應用程式使用的URI。 在 `com.adobe.primetime.reference.manager.EntitlementManger` 類，設定 `environmentUri` 變數 `STAGING_URI` 或 `PRODUCTION_URI` 具體取決於您正在使用的Mogfire身份驗證服務環境。

   >[!NOTE]
   >
   >提供的請求者ID(「REF」)只應與轉移環境一起使用。

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

1. 自定義MVPD選擇網格。

   內容提供程式選擇頁顯示用戶可以從中選擇的前九個MVPD的表。 應用程式從應用程式內與黃金時段驗證系統中與程式設計師整合的可用MVPD匹配的有序清單中抽取前九個MVPD。 主MVPD的有序清單在Mogine身份驗證系統的MVPD ID上，而不是MVPD顯示名稱上。 驗證主MVPD清單中的MVPD ID是否與與程式設計師帳戶整合的MVPD ID匹配非常重要，因為在某些情況下，ID在整個整合中可能不同。 下面是類中找到的主MVPD的有序清單 `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`。

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

   下表提供了如何使用主MVPD的有序清單的示例。 第一列列出與程式設計師整合的MVPD。 第二列是MVPD的（縮短）排序清單。 第三列是用於向用戶顯示前六個MVPD的結果清單。

   此示例使用前6個MVPD，而不是實際的9個MVPD，以使示例簡單。 注意結果清單如何包含前兩個清單的交集，並且與第二個清單的排序相同。 另外，請注意，AT&amp;T U韻文不在最終清單中，因為只採用前六個匹配的MVPD。

| 可用MVPD | 主MVPD | 顯示6個MVPD |
|--- |--- |--- |
| <ol><li>康卡斯特菲尼迪</li><li>TWC</li><li>媒體</li><li>RCN</li><li>碟</li><li>AT&amp;T U-verse</li><li>電纜1</li><li>光明屋</li><li>大西洋寬頻</li><li>哇！</li><li>地鐵</li><li>直播電視 </li><li>考克斯</li><li>最佳電纜</li></ol> | <ol><li>康卡斯特菲尼迪</li><li>直播電視</li><li>碟</li><li> TWC</li><li>考克斯</li><li>憲章</li><li>Verizon FiOS</li><li>最佳電纜</li><li>AT&amp;T U-verse</li></ol> | <ol><li>康卡斯特菲尼迪</li><li>直播電視</li><li>碟</li><li>TWC</li><li>考克斯</li><li>最佳電纜</li></ol> |
