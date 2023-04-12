---
title: Cookie更新 — SameSite和Secure標幟
description: Cookie更新 — SameSite和Secure標幟
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# Cookie更新 — SameSite和Secure標幟 {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>


## 更新 {#Updates}

本節重點說明Chrome瀏覽器和Adobe Primetime驗證為處理第三方Cookie所推出的變更。

 

### Chrome 80更新 {#Chrome}

從Chrome 80版開始（82版除外），未指定 *SameSite* 屬性會視為 *SameSite=Lax*. 因此，需要在跨網站內容中傳送的Cookie必須明確指定 *SameSite=None*，也必須加上 *安全* 屬性和傳遞 *HTTPS*. 有關這些更新的更多詳細資訊，請參閱官方的chromium頁面： <https://www.chromium.org/updates/same-site> 同時從 <https://web.dev/samesite-cookies-explained/>.


### Adobe Primetime驗證更新 {#Pass-Updates}

Adobe Primetime驗證服務目前依賴從瀏覽器觀點（包括Chrome）將兩個Cookie視為第三方Cookie，以搭配某些平台和Adobe Primetime驗證SDK版本運作。 因此，為了遵循即將進行的變更，並繼續從這些舊版SDK在跨網站內容中傳送這些Cookie,Adobe Primetime驗證服務會在 *adobe-pass-2.55.1* 版本。

這些變更來自 *adobe-pass-2.55.1* 版本涉及新增 *安全* 和 *SameSite=None* 從80版及更新版本開始使用Chrome瀏覽器時，其所有cookie都會傳回至所有Adobe Primetime驗證SDK的屬性（82版除外）。

下節將說明一些平台和Adobe Primetime驗證SDK版本清單的潛在問題，以防一位使用者使用Chrome瀏覽器80及以上版本（第82版除外）。

## 疑難排解 {#Troubleshooting}

瀏覽本節時，請記住所有Adobe Primetime驗證服務Cookie都必須 *安全* 屬性設定 *adobe-pass-2.55.1* 版本，若 *SameSite=None* 必須僅為Chrome瀏覽器80版及以上版本（82版除外）設定屬性。


### 一般疑難排解 {#General}

1. 請注意，某些使用者代理已知與 *SameSite=None* 屬性。

   - 從Chrome 51到Chrome 66的Chrome版本（兩端均包含）。 這些Chrome版本將拒絕具有 *SameSite=None*. 這也會影響舊版Chromium衍生瀏覽器以及Android WebView。 根據當時的Cookie規格版本，此行為是正確的，但在規格中加入新的「無」值後，Chrome 67及更新版本中就更新了此行為。 (在Chrome 51之前，會完全忽略SameSite屬性，而所有Cookie都會視為 *SameSite=None*.)
   - 12.13.2版之前的Android上的UC瀏覽器版本。舊版將拒絕具有的Cookie *SameSite=None*. 此行為根據當時的Cookie規格版本是正確的，但隨著規格新增「無」值，此行為已在較新版本的UC瀏覽器中更新。
   - MacOS 10.14上的Safari和內嵌瀏覽器版本，以及iOS 12上的所有瀏覽器。 這些版本會錯誤處理標示為的Cookie *SameSite=None* 就像是 *SameSite=Strict*. 較新版本的iOS和MacOS已修正此錯誤。


1. 請務必注意，Cookie具有 *安全* 屬性必須透過 *HTTPS*，否則Cookie將無法到達Adobe Primetime驗證服務。

   - AccessEnabler JavaScript SDK:
      - 強制要求與 *sp.auth.adobe.com* uses *HTTPS* 適用於版本 *2.35* 和 *3.5.0*，再推出動態用戶端註冊。
   - AccessEnabler iOS/tvOS SDK:
      - 強制要求與 *sp.auth.adobe.com* uses *HTTPS* 適用於舊版 *3.0.0*，再推出動態用戶端註冊。
   - AccessEnabler Android SDK:
      - 強制要求與 *sp.auth.adobe.com* uses *HTTPS* 適用於舊版 *3.0.0*，再推出動態用戶端註冊。
   - AccessEnabler FireOS SDK:
      - 強制要求與 *sp.auth.adobe.com* uses *HTTPS* 版本 *2.0.4*.

</br>

### AccessEnabler JavaScript SDK 2.35版疑難排解 {#235-Troubleshooting}

在Chrome 80及更新版本中（第82版除外），使用者的驗證流程可能會受到影響。 為了確保用戶沒有由於上述更新而遇到驗證問題，可以：

- 檢查 *JSESSIONID* cookie設定於瀏覽器中，且具有 *SameSite=None* 和 *安全* 屬性集。 
- 檢查 *JSESSIONID* cookie來自 *https://sp.auth.adobe.com/authenticate/saml* 網路請求符合 *JSESSIONID* cookie來自 *https://sp.auth.adobe.com/session* 網路要求。


### AccessEnabler JavaScript SDK 3.5.0版疑難排解 {#350-Troubleshooting}

在Chrome 80及更新版本中（第82版除外），使用者的驗證流程可能會受到影響。 為了確保用戶沒有由於上述更新而遇到驗證問題，可以：

- 檢查 *JSESSIONID* cookie設定於瀏覽器中，且具有 *SameSite=None* 和 *安全* 屬性集。 
- 檢查 *JSESSIONID* cookie來自 *https://sp.auth.adobe.com/authenticate/saml* 網路請求符合 *JSESSIONID* cookie來自 *https://sp.auth.adobe.com/session* 網路要求。
- 檢查 *pass\_sfp* cookie設定於瀏覽器中，且具有 *SameSite=None* 和 *安全* 屬性集。
- 檢查 *pass\_sfp* cookie設定於 *https://sp.auth.adobe.com/session* 網路要求。


在Chrome 80及更新版本中（第82版除外），使用者的授權流程可能會受到影響。 為了確保用戶在成功驗證後沒有出現監視受保護資源的問題，因為上述更新可以：

- 檢查 *pass\_sfp* cookie設定於瀏覽器中，且具有 *SameSite=None* 和 *安全* 屬性集。
- 檢查 *pass\_sfp* cookie設定於 *https://sp.auth.adobe.com/adobe-services/authorize* 網路要求。
- 檢查 *pass\_sfp* cookie設定於 *https://sp.auth.adobe.com/adobe-services/shortAuthorize* 網路要求。
