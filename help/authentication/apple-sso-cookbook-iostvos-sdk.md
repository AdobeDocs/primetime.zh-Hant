---
title: AppleSSO Cookbook(iOS/tvOS SDK)
description: AppleSSO Cookbook(iOS/tvOS SDK)
exl-id: 2d59cd33-ccfd-41a8-9697-1ace3165bc44
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---

# AppleSSO Cookbook(iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#Introduction}

Adobe Primetime驗證AccessEnableriOS/tvOS SDK可支援平台單點登錄(SSO)驗證，通過我們稱為AppleSSO工作流，為在iOS、iPadOS或tvOS上運行的客戶端應用程式的最終用戶提供此驗證。

請注意，此文檔是現有AccessEnableriOS/tvOS SDK文檔的擴展，可以找到 [這裡](/help/authentication/iostvos-sdk-api-reference.md)。

</br>

## 烹飪書 {#Cookbook}

為了從AppleSSO用戶體驗中獲益，一個應用程式需要整合AccessEnableriOS/tvOS SDK，並遵循下面介紹的提示順序。

</br>

### 先決條件 {#Prerequisites}

</br>

#### 權限

>[!TIP]
>
> **<u>專業提示：</u>** 為了能夠訪問用戶的訂閱資訊，用戶必須授予應用程式權限才能繼續，類似於提供對設備的攝像頭或麥克風的訪問。 每個應用程式都必須請求此權限，設備將保存用戶的選擇。 請記住，用戶可以通過轉到應用程式設定（電視提供商權限訪問）或從 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。

>[!TIP]
>
> **<u>專業提示：</u>** 我們建議在應用程式進入前台狀態時請求用戶的權限，但這只是建議，因為應用程式可以檢查 [訪問權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶的訂閱資訊在需要用戶身份驗證之前的任何時間點。 此外，AccessEnableriOS/tvOS SDK API將在需要時自動請求用戶的權限。

>[!TIP]
>
> **<u>專業提示：</u>** 如果用戶未授予對其訂閱資訊的訪問權限，或者在與視頻訂閱者帳戶框架的通信失敗時，AccessEnableriOS/tvOS SDK將回退到常規身份驗證流。

>[!TIP]
>
> **<u>專業提示：</u>** 我們建議通過解釋單一登錄(SSO)用戶體驗的優點來激勵拒絕授予訪問訂閱資訊權限的用戶。 請記住，用戶可以通過轉到應用程式設定（電視提供商權限訪問）或從 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### 回調

>[!TIP]
>
> **<u>專業提示：</u>** 實施以下清單 [回調](/help/authentication/iostvos-sdk-api-reference.md) 是AppleSSO工作流所特有的。

- [*presentTVProvider對話框*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) -AppleMVPD選取器開啟時觸發的回調。
- [*消除TVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) -AppleMVPD選取器即將關閉時觸發的回調。

</br>

#### 錯誤報告

>[!TIP]
>
> **<u>專業提示：</u>** 實施以下清單 [高級錯誤代碼](/help/authentication/error-reporting.md) 是AppleSSO工作流所特有的。

- ***N003***  — 用戶從AppleMVPD選取器中選擇了「其他電視提供商」選項。
- ***N004***  — 用戶從AppleMVPD選取器中選擇了TV Provider，當前請求者不支援該選取器（整合或單一登錄已禁用）。
- ***N005***  — 用戶決定取消常規MVPD選取器或AppleMVPD選取器。
- ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
- ***VSA404***  — 用戶對應用程式的電視提供程式權限未確定。
- ***VSA503***  — 視頻訂閱伺服器帳戶元資料請求失敗，在 *消息* 的子菜單。
- ***AAPL/APPL_ERROR***  — 視頻訂閱伺服器帳戶元資料請求失敗，在 *詳細資訊* 的子菜單。 

</br>

### 驗證 {#Authentication}

>[!TIP]
>
> **<u>提示：</u>** 按照以下步驟執行iOS/iPadOS/tvOS實施/s。

1. 申請必須 [初始化](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) AccessEnableriOS/tvOS SDK。
1. 申請必須 [設定當前請求者標識符](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3)。

   **重要提示：** 第二步可能會觸發 [高級錯誤代碼](/help/authentication/error-reporting.md) 這是特定於AppleSSO工作流的 **以下情況之一**:

   - ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
   - ***VSA404***  — 用戶對應用程式的電視提供程式權限未確定。
   - ***應用程式*** - AccessEnableriOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。

   第二步將嘗試以靜默方式交換AppleSSO配置檔案以用於Adobe身份驗證令牌，以防萬一 **以上所有的都是假的** 和 **以下所有內容均為真**:

   - 用戶的TV Provider權限已授予該應用程式。
   - 用戶在設備系統級別登錄到其電視提供商帳戶。
   - AccessEnableriOS/tvOS SDK從視頻訂閱者帳戶框架中接收了用戶的電視提供程式標識符。
   - 用戶的電視提供商與應用程式的整合通過Adobe PrimetimeTVE儀表板啟用。
   - 通過Adobe PrimetimeTVE儀表板啟用用戶的帶應用程式的電視提供商單點登錄。
   - 用戶的電視提供商未通過Adobe PrimetimeTVE儀表板降級。
   - AccessEnableriOS/tvOS SDK從視頻訂閱者帳戶框架接收了用戶的TV提供程式SAML響應。

   **<u>專業提示：</u>** 此第二步不會觸發任何其他回調，除 [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) 回調，因為驗證未由應用程式顯式啟動。

1. 申請必須 [檢查驗證狀態](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn)。

   **重要提示：** 第三步可能會觸發 [高級錯誤代碼](/help/authentication/error-reporting.md) 這是特定於AppleSSO工作流的 **以下情況之一**:

   - ***VSA403**  — 用戶已在設備系統級別登錄到其TV Provider帳戶，但拒絕用戶對該應用程式的TV Provider權限。
   - ***VSA404**  — 用戶在設備系統級別登錄到其電視提供程式帳戶，但用戶對應用程式的電視提供程式權限未確定。
   - ***APPL\_ERROR**  — 用戶已在設備系統級別登錄到其TV Provider帳戶，但AccessEnableriOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。

   **重要提示：** 第三步將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回調 *狀態* 等於0，在 **以下情況之一**:

   - 用戶未在設備系統級別或通過常規驗證流登錄到其電視提供商帳戶。
   - 用戶在設備系統級別或通過常規驗證流登錄到其TV Provider帳戶，但用戶的TV Provider驗證令牌TTL已通過。
   - 用戶在設備系統級別或通過常規驗證流登錄到其電視提供商帳戶，但用戶的電視提供商與應用程式的整合通過Adobe PrimetimeTVE儀表板被禁用。
   - 用戶在設備系統級別登錄到其電視提供商帳戶，但用戶與應用程式的電視提供商單一登錄通過Adobe PrimetimeTVE儀表板被禁用。
   - 用戶已在設備系統級別登錄到其TV Provider帳戶，但拒絕用戶對該應用程式的TV Provider權限。
   - 用戶在設備系統級別登錄到其電視提供程式帳戶，但用戶對應用程式的電視提供程式權限未確定。
   - 用戶已在設備系統級別登錄到其TV Provider帳戶，但AccessEnableriOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。

   **重要提示：** 第三步將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回調 *狀態* 等於1，在 **上述所有情況都是假的。**


1. 申請必須 [初始化身份驗證](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) 以防以前的身份驗證狀態檢查觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回調 *狀態* 等於0。

   **<u>專業提示：</u>** 實施以下AccessEnableriOS/tvOS SDK API之一 [getAuthentication（獲取身份驗證）](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) 或 [getAuthentication：篩選器](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter)。

   **重要提示：** 第四步可能觸發 [高級錯誤代碼](/help/authentication/error-reporting.md) 這是特定於AppleSSO工作流的 **以下情況之一**:

   - ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
   - ***VSA404***  — 用戶對應用程式的電視提供程式權限未確定。
   - ***VSA503*** - AccessEnableriOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。
   - ***N003***  — 用戶從AppleMVPD選取器中選擇了「其他電視提供商」選項。
   - ***N004***  — 用戶從AppleMVPD選取器中選擇了TV Provider，當前請求者不支援該選取器（整合或單一登錄已禁用）。
   - ***N005***  — 用戶決定取消常規MVPD選取器或AppleMVPD選取器。

   **重要提示：** 第四步將通過觸發 [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) 回調 **一個** 的 [高級錯誤代碼](/help/authentication/error-reporting.md)，在 **上述情況之一是**。 

   **重要提示：** 第四步將通過觸發 [導航至URL](/help/authentication/iostvos-sdk-api-reference.md#nav2url) 或 [導航至Url:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) 回調 **無** 的 [高級錯誤代碼](/help/authentication/error-reporting.md)，如果用戶選擇了不支援AppleSSO但存在於AppleMVPD選取器中的電視提供商。

   **<u>專業提示：</u>** AccessEnableriOS/tvOS SDK以靜默方式調用 [setSelectedProvder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API，如果用戶選擇了不支援AppleSSO但存在於AppleMVPD選取器中的電視提供商。

   **重要提示：** 第四步將嘗試以靜默方式交換AppleSSO配置檔案以用於Adobe身份驗證令牌，以防萬一 **以上所有的都是假的** 和 **以下所有內容均為真**:

   - 用戶的TV Provider權限已授予該應用程式。
   - 用戶已登錄/當前登錄到其設備系統級別的電視提供商帳戶。
   - AccessEnableriOS/tvOS SDK從視頻訂閱者帳戶框架中接收了用戶的電視提供程式標識符。
   - 用戶的電視提供商與應用程式的整合通過Adobe PrimetimeTVE儀表板啟用。
   - 通過Adobe PrimetimeTVE儀表板啟用用戶的帶應用程式的電視提供商單點登錄。
   - 用戶的電視提供商未通過Adobe PrimetimeTVE儀表板降級。
   - AccessEnableriOS/tvOS SDK從視頻訂閱者帳戶框架接收了用戶的TV提供程式SAML響應。


 

>**<u>專業提示：</u>** 第四步將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) 回調，無論 *狀態* 結果，因為驗證是由應用程式顯式啟動的。


</br>

### 元資料 {#Metadata}

應用程式可以選擇通過平台SSO登錄是否導致身份驗證，使用「 」*tokenSource&quot;* [用戶元資料](/help/authentication/iostvos-sdk-api-reference.md#getMeta) AccessEnableriOS/tvOS SDK中的API。

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### 註銷 {#Logout}

的 [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) framework不提供API以寫程式方式註銷在設備系統級別登錄到其電視提供商帳戶的人員。 因此，要使註銷完全生效，最終用戶必須明確註銷 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。 用戶必須具有的另一個選項是撤消從特定應用程式設定部分（電視提供程式權限訪問）訪問用戶訂閱資訊的權限。

>[!TIP]
>
> **<u>提示：</u>** 通過AccessEnableriOS/tvOS SDK介質實現此功能 [註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) API。


>[!TIP]
>
> **<u>專業提示：</u>** 請按照以下步驟執行tvOS實施。

- 申請必須 [啟動註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) 從AccessEnableriOS/tvOS SDK。 這無助於MVPD端的會話清理。
- 應用程式必須指示/提示用戶明確註銷 *`Settings -> Accounts -> TV Provider`* 只在情況下才能在電視OS上 [*VSA203* 狀態代碼已觸發](/help/authentication/error-reporting.md)。

>[!TIP]
>
> **<u>專業提示：</u>** 按照以下步驟執行iOS/iPadOS實施。

- 申請必須 [啟動註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) 從AccessEnableriOS/tvOS SDK。 這將有助於在MVPD端進行會話清理。
- 應用程式必須指示/提示用戶明確註銷 *`Settings -> TV Provider`* 在iOS/iPadOS上，只在萬一 [*VSA203* 狀態代碼已觸發](/help/authentication/error-reporting.md)。


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
