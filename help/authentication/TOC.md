---
product: adobe primetime
audience: end-user
user-guide-title: Primetime驗證
user-guide-description: Primetime驗證是TV Everywhere的權限解決方案，提供模組化架構，以判斷要求存取資源的人是否有權使用資源。
source-git-commit: 0afc48ae0e423c2a851b3bf22803fbd730999c04
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---


# Primetime驗證說明 {#authentication}

+ [Primetime驗證概述](home.md)
+ Primetime驗證概念 {#authentication-concepts}
   + [技術檔案](technical-paper.md)
   + [程式設計人員概覽](programmer-overview.md)
   + [MVPD概述](mvpd-overview.md)
+ 副標題指南 {#kickstart-guides}
   + [程式設計師啟動指南](programmer-kickstart-guide.md)
   + [MVPD啟動指南](mvpd-kickstart-guide.md)
+ 程式設計師整合指南 {#programmer-integration-guide}
   + [程式設計師整合指南概述](programmer-integration-guide-overview.md)
   + [程式設計師權利流程](entitlement-flow.md)
   + [程式設計師使用案例](programmer-use-cases.md)
   + [傳遞客戶端資訊（設備、連接和應用程式）](passing-client-information-device-connection-and-application.md)
   + REST API {#restapi}
      + [REST API概述](rest-api-overview.md)
      + [REST API逐步指南（伺服器對伺服器）](rest-api-cookbook-servertoserver.md)
      + [REST API逐步指南（用戶端對伺服器）](rest-api-cookbook-clienttoserver.md)
      + Rest API參考 {#rest-api-reference}
         + [REST API參考](rest-api-reference.md)
         + [註冊代碼請求](registration-code-request.md)
         + [返回註冊記錄](return-registration-record.md)
         + [刪除註冊記錄](delete-registration-record.md)
         + [提供MVPD清單](provide-mvpd-list.md)
         + [啟動驗證](initiate-authentication.md)
         + [檢查驗證Token](check-authentication-token.md)
         + [擷取驗證Token](retrieve-authentication-token.md)
         + [啟動授權](initiate-authorization.md)
         + [擷取授權Token](retrieve-authorization-token.md)
         + [取得短媒體代號](obtain-short-media-token.md)
         + [按第二螢幕Web應用檢查驗證流](check-authentication-flow-by-second-screen-web-app.md)
         + [檢索預授權資源清單](retrieve-list-of-preauthorized-resources.md)
         + [按第二螢幕Web應用檢索預授權資源清單](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [啟動註銷](initiate-logout.md)
         + [使用者中繼資料](user-metadata.md)
         + [擷取設定檔請求](retrieve-profilerequest.md)
         + [代號交換](token-exchange.md)
         + [臨時通行證和促銷臨時通行證的免費預覽](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + AccessEnabler SDK {#accessenabler-sdk}
      + JavaScript SDK {#javascriptsdk}
         + [JavaScript SDK概述](javascript-sdk-overview.md)
         + [JavaScript SDK逐步指南](javascript-sdk-cookbook.md)
         + [JavaScript SDK API參考](javascript-sdk-api-reference.md)
         + 准則 {#js-sdk-guidelines}
            + [無刷新登錄和註銷](refreshless-login-and-logout.md)
         + JavaScript API {#js-api}
            + [預先授權](js-preauthorize.md)
      + iOS/tvOS SDK {#ios-sdk}
         + [iOS/tvOS SDK概述](iostvos-sdk-overview.md)
         + [iOS/tvOS SDK逐步指南](iostvos-sdk-cookbook.md)
         + [iOS/tvOS SDK API參考](iostvos-sdk-api-reference.md)
         + 准則 {#ios-tvos-sdk-guidelines}
            + [iOS/tvOS應用程式註冊](iostvos-application-registration.md)
            + 移轉准則 {#migration-guidelines}
               + [iOS/tvOS v3.x移轉指南](iostvos-v3x-migration-guide.md)
         + iOS/tvOS API {#ios-tvos-api}
            + [預先授權](preauthorize.md)
      + Android SDK {#androidsdk}
         + [Android SDK概述](android-sdk-overview.md)
         + [Android SDK逐步指南](android-sdk-cookbook.md)
         + [Android SDK API參考](android-sdk-api-reference.md)
         + 准則 {#androidguidelines}
            + [Android應用程式註冊](android-application-registration.md)
            + [具有動態用戶端註冊的Android SDK](android-sdk-with-dynamic-client-registration.md)
         + Android API{#androidapi}
            + [預先授權](preauthorize-android.md)
      + Amazon FireOS SDK {#fireossdk}
         + [Amazon FireOS SSO — 程式設計師啟動指南](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [Amazon FireOS SSO（使用無用戶端API逐步指南）](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [Amazon FireOS技術概述](amazon-fireos-technical-overview.md)
         + [Amazon FireOS整合逐步指南](amazon-fireos-integration-cookbook.md)
         + [Amazon FireOS API參考](amazon-fireos-native-client-api-reference.md)
         + [Amazon FireOS應用程式註冊](amazon-fireos-application-registration.md)
         + [具有動態用戶端註冊的FireOS SDK](fireos-sdk-with-dynamic-client-registration.md)
   + 平台SSO {#platform-sso}
      + AppleSSO {#apple-sso}
         + [Apple SSO概述](apple-sso-overview.md)
         + [Apple SSO逐步指南(REST API)](apple-sso-cookbook-rest-api.md)
         + [Apple SSO逐步指南(iOS/tvOS SDK)](apple-sso-cookbook-iostvos-sdk.md)
      + Roku SSO {#roku-sso}
         + [Roku SSO](roku-sso-overview.md)
   + 內容中繼資料 {#content-metadata}
      + [標識受保護的資源](identify-protected-resources.md)
   + 內容伺服器整合 {#content-serv-int}
      + [如何整合媒體代號驗證器](media-token-verifier-int.md)
   + 附錄 {#appendices}
      + [除錯提示](appendix-b-debugging-tips.md)
+ MVPD整合指南 {#mvpd-int-guide}
   + [整合功能](mvpd-integr-features.md)
   + [驗證](authn-usecase.md)
   + [使用OAuth 2.0通訊協定進行驗證](authn-oauth2-protocol.md)
   + [授權](authz-usecase.md)
   + [飛行前授權](mvpd-preflight-authz.md)
   + [MVPD註銷](usecase-mvpd-logout.md)
   + [內容中繼資料交換](mvpd-content-metadata-exchange.md)
   + [用戶元資料交換](mvpd-user-metadata-exchng.md)
   + [代理MVPD Web服務](proxy-mvpd-webserv.md)
   + [代理MVPD SAML整合](proxy-mvpd-saml-int.md)
   + [服務提供商範圍](serv-provider-scoping.md)
   + [MVPD允許IP位址](mvpd-listing-ip-addres.md)
+ Primetime驗證功能 {#auth-features}
   + Adobe Analytics整合 {#analytics-int}
      + [將Primetime驗證伺服器端資料整合至Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [在Primetime驗證中使用Experience CloudID](exp-cloud-id-authn.md)
   + 權利服務監控 {#entitlement-service-monitoring}
      + [權利服務監視概述](entitlement-service-monitoring-overview.md)
      + [權益服務監視API](entitlement-service-monitoring-api.md)
      + [伺服器端量度](understanding-serverside-metrics.md)
   + 臨時通道 {#temp-pass}
      + [臨時通道](temp-pass.md)
      + [促銷臨時通道](promotional-temp-pass.md)
   + 單一登入 {#sso}
      + [單一登入支援](sso-support.md)
      + [通過被動身份驗證的SSO](sso-passive-authn.md)
   + 基於家庭的身份驗證 {#home-based-auth}
      + [基於家庭的TV Everywhere驗證](home-based-authn-tve.md)
      + [MVPD的HBA狀態](hba-status-mvpds.md)
   + 使用者中繼資料 {#user-metadat}
      + [使用者中繼資料](user-metadata-feature.md)
   + [飛行前授權](preflight-authz.md)
   + 錯誤報告 {#error-reportn}
      + [錯誤報告](error-reporting.md)
      + [增強的錯誤代碼](enhanced-error-codes.md)
   + 客戶端註冊 {#client-regn}
      + [動態客戶端註冊](dynamic-client-registration.md)
      + [動態用戶端註冊API](dynamic-client-registration-api.md)
      + [Dynamic Client註冊管理](dynamic-client-registration-management.md)
   + 退化服務 {#degrn-service}
      + [降級API概述](degradation-api-overview.md)
   + 隱私權準備 {#privacy-readiness}
      + [隱私權支援概觀](privacy-supp-overview.md)
      + [如何提出隱私權要求](make-privacy-req.md)
+ 提示與疑難排解 {#tips-troubleshoot}
   + [在選取對話方塊中允許MVPD](allow-mvpd-selectn-dialog.md)
   + [防止MVPD顯示選取對話方塊](prevent-mvpd-selectn-dialog.md)
+ 支援 {#support}
   + [呈報程式](escalation-procedures.md)
   + [監控PrimetimeAdobePayTV通道](monitoring-adobe-pay-tv-pass.md)
   + [最低系統需求](minimum-system-requirements.md)
+ 發行說明 {#release-notes}
   + [Primetime驗證2.64.1發行說明](auth-rn-2641.md)
   + [Primetime Authentication 2.64發行說明](auth-rn-264.md)
   + [Primetime Authentication 2.63發行說明](auth-rn-263.md)
   + [Primetime驗證2.62.1發行說明](auth-rn-2621.md)
   + [Primetime驗證iOS / tvOS 3.7.0發行說明](authn-rn-ios-tvos-370.md)
+ 技術說明 {#tech-notes}
   + Primetime驗證SDK {#primetime-authentication-sdks}
      + [證書問答](certificates-qa.md)
      + JavaScript SDK {#javascript}
         + [Safari瀏覽器的JS SDK限制](js-sdk-limitations-for-safari-browser.md)
         + [Cookie更新 — SameSite和Secure標幟](cookies-updates--samesite-and-secure-flags.md)
      + Android SDK {#android}
         + [在Android 10應用程式上存取啟用碼Android SDK單一登入(SSO)](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Adobe Primetime驗證與Android 6「Marshmallow」新權限模型](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + iOS/tvOS SDK {#iostvos}
         + [iOS SDK 3.1以上版本的WKWebView支援](wkwebview-support-on-ios-sdk-31.md)
         + [iOS SDK 3.2+上的SFSafariViewController支援](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [使用Primetime驗證存取啟用碼時在iOS上的SSO](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [iOS驗證錯誤 — 找不到adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [在iOS上重設Temp Pass](reset-temp-pass-on-ios.md)
         + [使用主控台應用程式記錄檔對AccessEnabler iOS/tvOS SDK除錯](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [AccessEnabler iOS/tvOS 3.7.0升級路徑](accessenabler-iostvos-370-upgrade-path.md)
   + Primetime驗證環境 {#primetime-authentication-environments}
      + [了解Adobe環境](understanding-the-adobe-environments.md)
      + [在準年前設定您的環境和測試](setting-up-your-environment-and-testing-in-prequal.md)
      + [如何使用AdobeAPI測試網站來測試驗證和授權流程](test-authn-authz-flows-using-adobes-api-test-site.md)
   + 無用戶端API {#clientless-api}
      + [無用戶端API實作 — 錯誤碼/可能原因/原因的訊息](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [沒有裝置ID時的無用戶端API流程](clientless-api-flow-in-the-absence-of-device-id.md)
      + [無客戶端：避免在/authenticate請求中使用&#39;&amp;&#39;reg_code](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [為Xbox 360和XboxOne無客戶端上的程式啟用Primetime權限服務](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [無用戶端裝置類型和量度](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + 使用者體驗 {#user-exp}
      + [如何將MVPD登入頁面從iFrame移轉至快顯視窗](migr-mvpd-login-iframe-popup.md)
      + [預檢功能：如何啟用、疑難排解或判斷問題](preflight-feature.md)
   + 工具和實用程式 {#tools-and-utilities}
      + [使用Charles Proxy](using-charles-proxy.md)
   + 概念 {#concepts}
      + [了解使用者ID](understanding-user-ids.md)
+ [TVE儀表板使用手冊](tve-dashboard-user-guide.md)
+ [字彙表](glossary.md)
