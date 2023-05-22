---
product: adobe primetime
audience: end-user
user-guide-title: 黃金時段身份驗證
user-guide-description: 黃金時段身份驗證是TV Everywhere的權利解決方案，它提供了一個模組化框架，用於確定請求訪問資源的人是否有權訪問資源。
source-git-commit: aa8169da1308e5372128a93b6a2e5a3a6db5cfef
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# 黃金時段身份驗證幫助 {#authentication}

+ [黃金時段身份驗證概述](home.md)
+ 黃金時段驗證概念 {#authentication-concepts}
   + [技術檔案](technical-paper.md)
   + [程式設計師概述](programmer-overview.md)
   + [MVPD概述](mvpd-overview.md)
+ 踢球指南 {#kickstart-guides}
   + [程式設計師啟動指南](programmer-kickstart-guide.md)
   + [MVPD啟動指南](mvpd-kickstart-guide.md)
+ 程式設計師整合指南 {#programmer-integration-guide}
   + [程式設計師整合指南概述](programmer-integration-guide-overview.md)
   + [程式設計師權利流](entitlement-flow.md)
   + [程式設計師使用案例](programmer-use-cases.md)
   + [傳遞客戶端資訊（設備、連接和應用程式）](passing-client-information-device-connection-and-application.md)
   + REST API {#restapi}
      + [REST API概述](rest-api-overview.md)
      + [REST API指南（伺服器到伺服器）](rest-api-cookbook-servertoserver.md)
      + [REST API指南（客戶端到伺服器）](rest-api-cookbook-clienttoserver.md)
      + REST API參考 {#rest-api-reference}
         + [REST API參考](rest-api-reference.md)
         + [註冊代碼請求](registration-code-request.md)
         + [返回註冊記錄](return-registration-record.md)
         + [刪除註冊記錄](delete-registration-record.md)
         + [提供MVPD清單](provide-mvpd-list.md)
         + [啟動身份驗證](initiate-authentication.md)
         + [檢查驗證令牌](check-authentication-token.md)
         + [檢索身份驗證令牌](retrieve-authentication-token.md)
         + [啟動授權](initiate-authorization.md)
         + [檢索授權令牌](retrieve-authorization-token.md)
         + [獲取短媒體令牌](obtain-short-media-token.md)
         + [按第二螢幕Web應用檢查身份驗證流](check-authentication-flow-by-second-screen-web-app.md)
         + [檢索預授權資源清單](retrieve-list-of-preauthorized-resources.md)
         + [按第二螢幕Web應用檢索預授權資源清單](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [啟動註銷](initiate-logout.md)
         + [用戶元資料](user-metadata.md)
         + [檢索配置檔案請求](retrieve-profilerequest.md)
         + [令牌交換](token-exchange.md)
         + [臨時通行證和促銷臨時通行證的免費預覽](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + AccessEnabler SDK {#accessenabler-sdk}
      + JavaScript SDK {#javascriptsdk}
         + [JavaScript SDK概述](javascript-sdk-overview.md)
         + [JavaScript SDK指南](javascript-sdk-cookbook.md)
         + [JavaScript SDK API參考](javascript-sdk-api-reference.md)
         + 准則 {#js-sdk-guidelines}
            + [無刷新登錄和註銷](refreshless-login-and-logout.md)
         + JavaScript API {#js-api}
            + [預授權](js-preauthorize.md)
      + iOS/電視作業系統SDK {#ios-sdk}
         + [iOS/tvOS SDK概述](iostvos-sdk-overview.md)
         + [iOS/電視OS SDK指南](iostvos-sdk-cookbook.md)
         + [iOS/tvOS SDK API參考](iostvos-sdk-api-reference.md)
         + 准則 {#ios-tvos-sdk-guidelines}
            + [iOS/tvOS應用程式註冊](iostvos-application-registration.md)
            + 遷移准則 {#migration-guidelines}
               + [iOS/電視OS v3.x遷移指南](iostvos-v3x-migration-guide.md)
         + iOS/電視OS API {#ios-tvos-api}
            + [預授權](preauthorize.md)
      + Android SDK {#androidsdk}
         + [Android SDK概述](android-sdk-overview.md)
         + [Android SDK指南](android-sdk-cookbook.md)
         + [Android SDK API參考](android-sdk-api-reference.md)
         + 准則 {#androidguidelines}
            + [Android應用程式註冊](android-application-registration.md)
            + [帶動態客戶端註冊的Android SDK](android-sdk-with-dynamic-client-registration.md)
         + Android API{#androidapi}
            + [預授權](preauthorize-android.md)
      + AmazonFireOS SDK {#fireossdk}
         + [AmazonFireOS SSO — 程式設計師啟動指南](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [AmazonFireOS SSO使用無客戶端API指南](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [AmazonFireOS技術概述](amazon-fireos-technical-overview.md)
         + [AmazonFireOS整合指南](amazon-fireos-integration-cookbook.md)
         + [AmazonFireOS API參考](amazon-fireos-native-client-api-reference.md)
         + [AmazonFireOS應用程式註冊](amazon-fireos-application-registration.md)
         + [具有動態客戶端註冊的FireOS SDK](fireos-sdk-with-dynamic-client-registration.md)
   + 平台SSO {#platform-sso}
      + Apple {#apple-sso}
         + [AppleSSO概述](apple-sso-overview.md)
         + [AppleSSO Cookbook(REST API)](apple-sso-cookbook-rest-api.md)
         + [AppleSSO Cookbook(iOS/tvOS SDK)](apple-sso-cookbook-iostvos-sdk.md)
      + 羅庫索 {#roku-sso}
         + [羅庫索](roku-sso-overview.md)
   + 內容元資料 {#content-metadata}
      + [標識受保護的資源](identify-protected-resources.md)
   + Content Server整合 {#content-serv-int}
      + [如何整合媒體令牌驗證器](media-token-verifier-int.md)
   + 附錄 {#appendices}
      + [調試提示](appendix-b-debugging-tips.md)
+ MVPD整合指南 {#mvpd-int-guide}
   + [整合功能](mvpd-integr-features.md)
   + [驗證](authn-usecase.md)
   + [使用OAuth 2.0協定進行身份驗證](authn-oauth2-protocol.md)
   + [授權](authz-usecase.md)
   + [印前檢查授權](mvpd-preflight-authz.md)
   + [MVPD註銷](usecase-mvpd-logout.md)
   + [內容元資料交換](mvpd-content-metadata-exchange.md)
   + [用戶元資料交換](mvpd-user-metadata-exchng.md)
   + [代理MVPD Web服務](proxy-mvpd-webserv.md)
   + [代理MVPD SAML整合](proxy-mvpd-saml-int.md)
   + [服務提供商範圍界定](serv-provider-scoping.md)
   + [MVPD允許IP地址](mvpd-listing-ip-addres.md)
+ 黃金時段身份驗證功能 {#auth-features}
   + Adobe Analytics整合 {#analytics-int}
      + [將黃金時段身份驗證伺服器端資料整合到Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [在黃金時段Experience Cloud中使用身份驗證ID](exp-cloud-id-authn.md)
   + 權利服務監視 {#entitlement-service-monitoring}
      + [權利服務監視概述](entitlement-service-monitoring-overview.md)
      + [權利服務監視API](entitlement-service-monitoring-api.md)
      + [伺服器端度量](understanding-serverside-metrics.md)
   + 臨時通道 {#temp-pass}
      + [臨時通道](temp-pass.md)
      + [促銷臨時通行證](promotional-temp-pass.md)
   + 一次登錄 {#sso}
      + [單一登錄支援](sso-support.md)
      + [通過被動身份驗證的SSO](sso-passive-authn.md)
   + 基於家庭的身份驗證 {#home-based-auth}
      + [基於家庭的TV Everywhere身份驗證](home-based-authn-tve.md)
      + [MVPD的HBA狀態](hba-status-mvpds.md)
   + 用戶元資料 {#user-metadat}
      + [用戶元資料](user-metadata-feature.md)
   + [印前檢查授權](preflight-authz.md)
   + 報告錯誤 {#error-reportn}
      + [報告錯誤](error-reporting.md)
      + [增強的錯誤代碼](enhanced-error-codes.md)
   + 客戶端註冊 {#client-regn}
      + [動態客戶端註冊](dynamic-client-registration.md)
      + [動態客戶端註冊API](dynamic-client-registration-api.md)
      + [動態客戶端註冊管理](dynamic-client-registration-management.md)
   + 降級服務 {#degrn-service}
      + [降級API概述](degradation-api-overview.md)
   + 隱私準備 {#privacy-readiness}
      + [隱私支援概述](privacy-supp-overview.md)
      + [如何發出隱私請求](make-privacy-req.md)
+ 提示和故障排除 {#tips-troubleshoot}
   + [在選擇對話框中允許MVPD](allow-mvpd-selectn-dialog.md)
   + [阻止MVPD顯示選擇對話框](prevent-mvpd-selectn-dialog.md)
+ 支援 {#support}
   + [升級過程](escalation-procedures.md)
   + [監控黃金時段AdobePayTV Pass](monitoring-adobe-pay-tv-pass.md)
   + [最低系統要求](minimum-system-requirements.md)
+ 發行說明 {#release-notes}
   + [《黃金時段身份驗證2.65發行說明》](auth-rn-265.md)
   + [《 Mighine Authentication 2.64.1發佈說明》](auth-rn-2641.md)
   + [《黃金時段身份驗證2.64發行說明》](auth-rn-264.md)
   + [《黃金時段身份驗證2.63發行說明》](auth-rn-263.md)
   + [《 Mighine Authentication 2.62.1發佈說明》](auth-rn-2621.md)
   + [黃金時段身份驗證iOS/tvOS 3.7.0發行說明](authn-rn-ios-tvos-370.md)
+ 技術說明 {#tech-notes}
   + 黃金時段驗證SDK {#primetime-authentication-sdks}
      + [證書問答](certificates-qa.md)
      + JavaScript SDK {#javascript}
         + [Safari瀏覽器的JS SDK限制](js-sdk-limitations-for-safari-browser.md)
         + [Cookie更新 — SameSite和Secure標誌](cookies-updates--samesite-and-secure-flags.md)
      + Android SDK {#android}
         + [Access Enabler Android SDK Single Sign-On(SSO)，在Android 10應用上](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Adobe Primetime認證與Android 6「棉花糖」新權限模型](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + iOS/電視作業系統SDK {#iostvos}
         + [iOSSDK 3.1+上的WKWebView支援](wkwebview-support-on-ios-sdk-31.md)
         + [iOSSDK 3.2+上的SFSafariViewController支援](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [iOS上使用黃金時段身份驗證Access Enabler時的SSO](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [iOS驗證錯誤 — 找不到adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [重置臨時傳遞iOS](reset-temp-pass-on-ios.md)
         + [使用控制台應用日誌調試AccessEnableriOS/tvOS SDK](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [AccessEnableriOS/tvOS 3.7.0升級路徑](accessenabler-iostvos-370-upgrade-path.md)
   + 黃金時段身份驗證環境 {#primetime-authentication-environments}
      + [瞭解Adobe環境](understanding-the-adobe-environments.md)
      + [在準年前設定環境和測試](setting-up-your-environment-and-testing-in-prequal.md)
      + [如何使用testAPItest站點Adobe驗證和授權流](test-authn-authz-flows-using-adobes-api-test-site.md)
   + 無客戶端API {#clientless-api}
      + [無客戶端API實施 — 錯誤代碼/可能原因/原因的消息](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [沒有設備ID時的無客戶端API流](clientless-api-flow-in-the-absence-of-device-id.md)
      + [無客戶端：避免在/authenticate請求中使用&#39;&amp;&#39;reg_code](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [為Xbox 360和XboxOne無客戶端上的程式設計師啟用黃金時段權利服務](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [無客戶端設備類型和度量](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + 用戶體驗 {#user-exp}
      + [如何將MVPD登錄頁從iFrame遷移到彈出窗口](migr-mvpd-login-iframe-popup.md)
      + [印前檢查功能：如何啟用、排除故障或確定問題](preflight-feature.md)
   + 工具和實用程式 {#tools-and-utilities}
      + [使用Charles Proxy](using-charles-proxy.md)
   + 概念 {#concepts}
      + [瞭解用戶ID](understanding-user-ids.md)
+ [TVE儀表板使用手冊](tve-dashboard-user-guide.md)
+ [辭彙表](glossary.md)
