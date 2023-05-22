---
title: Cookie更新 — SameSite和Secure標誌
description: Cookie更新 — SameSite和Secure標誌
exl-id: cc1f60fd-fa64-48cb-a185-dba562a54c33
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Cookie更新 — SameSite和Secure標誌 {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>


## 更新 {#Updates}

本節重點介紹Chrome瀏覽器和Adobe Primetime身份驗證為處理第三方Cookie而引入的更改。

 

### Chrome 80更新 {#Chrome}

從Chrome版本80（版本82除外）開始，不指定 *同一站點* 屬性將被視為 *SameSite=Lax*。 因此，需要在跨站點上下文中傳遞的Cookie必須顯式指定 *SameSite=無*，並且必須標有 *安全* 屬性和交付 *HTTPS*。 有關這些更新的更多詳細資訊，可從官方鉻版上閱讀： <https://www.chromium.org/updates/same-site> 還有 <https://web.dev/samesite-cookies-explained/>。


### Adobe Primetime驗證更新 {#Pass-Updates}

Adobe Primetime認證服務目前依賴從瀏覽器的視角（包括Chrome）認為是第三方Cookie的兩個Cookie，以便與一些平台和Adobe Primetime認證SDK版本結合使用。 因此，為了遵守即將進行的更改並繼續在跨站點上下文中從這些較舊的SDK傳遞這些Cookie,Adobe Primetime身份驗證服務在 *adobe-pass-2.55.1* 。

這些更改 *adobe-pass-2.55.1* 版本涉及添加 *安全* 和 *SameSite=無* 使用從80版及更高版本開始的Chrome瀏覽器（除82版外）時，其所有Cookie的屬性傳回到所有Adobe Primetime驗證SDK。

下一節介紹平台清單和Adobe Primetime驗證SDK版本的一些潛在問題，以防一個用戶使用Chrome瀏覽器80及更高版本（版本82除外）。

## 故障排除 {#Troubleshooting}

瀏覽此部分時，請記住所有Adobe Primetime身份驗證服務Cookie必須 *安全* 屬性集 *adobe-pass-2.55.1* 版本，而 *SameSite=無* 只能為Chrome瀏覽器版本80及更高版本（版本82除外）設定屬性。


### 常規故障排除 {#General}

1. 請注意，已知某些用戶代理與 *SameSite=無* 屬性。

   - 從Chrome 51到Chrome 66的Chrome版本（兩端均包括）。 這些Chrome版本將拒絕Cookie *SameSite=無*。 這還影響到舊版的鉻衍生瀏覽器以及Android WebView。 根據當時的Cookie規範版本，此行為是正確的，但是，在規範中添加新的「無」值後，此行為已在Chrome 67和更新版本中更新。 (在Chrome 51之前， SameSite屬性被完全忽略，所有Cookie都被視為 *SameSite=無*。)
   - 12.13.2版之前的Android上的UC瀏覽器版本。舊版本將拒絕Cookie *SameSite=無*。 根據當時的Cookie規範版本，此行為是正確的，但是，在規範中添加新的「無」值後，此行為已在較新版本的UC瀏覽器中更新。
   - MacOS10.14上的Safari和嵌入式瀏覽器版本，以及iOS12上的所有瀏覽器。 這些版本將錯誤地處理標有Cookie *SameSite=無* 就像是標籤了 *SameSite=Strict*。 此Bug已在iOS和MacOS的新版本上修復。


1. 請注意， *安全* 必須將屬性發送 *HTTPS*，否則cookie將無法到達Adobe Primetime身份驗證服務。

   - AccessEnabler JavaScript SDK:
      - 強制要求與 *sp.auth.adobe.com* 使用 *HTTPS* 版本 *二點三五* 和 *3.5.0*，然後再引入動態客戶端註冊。
   - AccessEnableriOS/tvOS SDK:
      - 強制要求與 *sp.auth.adobe.com* 使用 *HTTPS* 對於以前的版本 *3.0.0*，然後再引入動態客戶端註冊。
   - AccessEnabler Android SDK:
      - 強制要求與 *sp.auth.adobe.com* 使用 *HTTPS* 對於以前的版本 *3.0.0*，然後再引入動態客戶端註冊。
   - AccessEnabler FireOS SDK:
      - 強制要求與 *sp.auth.adobe.com* 使用 *HTTPS* 版本 *2.0.4*。

</br>

### AccessEnabler JavaScript SDK版本2.35疑難解答 {#235-Troubleshooting}

在Chrome 80及更高版本（版本82除外）中，用戶的驗證流可能受到影響。 為了確保用戶沒有因上述更新而出現驗證問題，可以：

- 檢查 *JSESSIONID* cookie在瀏覽器中設定，並 *SameSite=無* 和 *安全* 屬性集。 
- 檢查 *JSESSIONID* 餅乾 *https://sp.auth.adobe.com/authenticate/saml* 網路請求與 *JSESSIONID* 餅乾 *https://sp.auth.adobe.com/session* 網路請求。


### AccessEnabler JavaScript SDK 3.5.0版疑難解答 {#350-Troubleshooting}

在Chrome 80及更高版本（版本82除外）中，用戶的驗證流可能受到影響。 為了確保用戶沒有因上述更新而出現驗證問題，可以：

- 檢查 *JSESSIONID* cookie在瀏覽器中設定，並 *SameSite=無* 和 *安全* 屬性集。 
- 檢查 *JSESSIONID* 餅乾 *https://sp.auth.adobe.com/authenticate/saml* 網路請求與 *JSESSIONID* 餅乾 *https://sp.auth.adobe.com/session* 網路請求。
- 檢查 *傳遞\_sfp* cookie在瀏覽器中設定，並 *SameSite=無* 和 *安全* 屬性集。
- 檢查 *傳遞\_sfp* cookie設定在 *https://sp.auth.adobe.com/session* 網路請求。


在Chrome 80及更高版本（版本82除外）中，用戶的授權流可能受到影響。 為了確保用戶在觀看受保護的資源時沒有遇到問題，在成功驗證後，由於上述更新，可以：

- 檢查 *傳遞\_sfp* cookie在瀏覽器中設定，並 *SameSite=無* 和 *安全* 屬性集。
- 檢查 *傳遞\_sfp* cookie設定在 *https://sp.auth.adobe.com/adobe-services/authorize* 網路請求。
- 檢查 *傳遞\_sfp* cookie設定在 *https://sp.auth.adobe.com/adobe-services/shortAuthorize* 網路請求。
