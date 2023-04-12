---
title: Apple SSO逐步指南(iOS/tvOS SDK)
description: Apple SSO逐步指南(iOS/tvOS SDK)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Apple SSO逐步指南(iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#Introduction}

Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可透過我們稱為Apple SSO工作流程，支援在iOS、iPadOS或tvOS上執行之用戶端應用程式的一般使用者平台單一登入(SSO)驗證。

請注意，本檔案是現有AccessEnabler iOS/tvOS SDK檔案的擴充功能，可從 [此處](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## 逐步指南 {#Cookbook}

為了從Apple SSO用戶體驗中受益，一個應用程式需要整合AccessEnabler iOS/tvOS SDK，並遵循以下提示的順序。

</br>

### 必要條件 {#Prerequisites}

</br>

#### 權限

>[!TIP]
>
> **<u>專業提示：</u>** 為了能夠訪問用戶的訂閱資訊，用戶必須授予應用程式繼續的權限，類似於提供對設備的攝像頭或麥克風的訪問。 必須按應用程式請求此權限，設備將保存用戶的選擇。 請記住，使用者可以前往應用程式設定（電視提供者權限存取）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

>[!TIP]
>
> **<u>專業提示：</u>** 我們建議在應用程式進入前景狀態時請求使用者的權限，但這只是建議，因為應用程式可以檢查 [存取權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶在需要用戶驗證之前的任何時間點的訂閱資訊。 此外， AccessEnabler iOS/tvOS SDK API將在需要時自動請求用戶的權限。

>[!TIP]
>
> **<u>專業提示：</u>** 如果使用者未授與其訂閱資訊的存取權，或者如果與視訊訂閱者帳戶架構的通訊失敗，AccessEnabler iOS/tvOS SDK將回退至一般驗證流程。

>[!TIP]
>
> **<u>專業提示：</u>** 建議您說明單一登入(SSO)使用者體驗的優點，以鼓勵拒絕授予存取訂閱資訊權限的使用者。 請記住，使用者可以前往應用程式設定（電視提供者權限存取）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。


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

#### 回呼

>[!TIP]
>
> **<u>專業提示：</u>** 實作下列清單 [回撥](/help/authentication/iostvos-sdk-api-reference.md) 這是Apple SSO工作流程專屬的。

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) -Apple MVPD選取器即將開啟時觸發回呼。
- [*discupsTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) -Apple MVPD選取器即將關閉時觸發回呼。

</br>

#### 錯誤報告

>[!TIP]
>
> **<u>專業提示：</u>** 實作下列清單 [高級錯誤代碼](/help/authentication/error-reporting.md) 這是Apple SSO工作流程專屬的。

- ***N003***  — 使用者從Apple MVPD選擇器中選取「其他電視提供者」選項。
- ***N004***  — 使用者從Apple MVPD選擇器中選取了電視提供者，目前要求者不支援（已停用整合或單一登入）。
- ***N005***  — 使用者決定取消一般的MVPD選擇器或Apple MVPD選擇器。
- ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
- ***VSA404***  — 未確定應用程式的用戶的電視提供商權限。
- ***VSA503***  — 視訊訂閱者帳戶中繼資料請求失敗， *訊息* 欄位。
- ***AAPL / APPL_ERROR***  — 視訊訂閱者帳戶中繼資料請求失敗， *詳細資訊* 欄位。 

</br>

### 驗證 {#Authentication}

>[!TIP]
>
> **<u>提示：</u>** 請依照下列步驟操作iOS/iPadOS/tvOS實作。

1. 申請必須 [初始化](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) accessEnabler iOS/tvOS SDK。
1. 申請必須 [設定當前請求者標識符](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **重要：** 第二步可能會觸發 [進階錯誤代碼](/help/authentication/error-reporting.md) 這是Apple SSO工作流程專屬的，若是 **以下其中一項是true**:

   - ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
   - ***VSA404***  — 未確定應用程式的用戶的電視提供商權限。
   - ***APPL*** - AccessEnabler iOS/tvOS SDK與視訊訂閱者帳戶架構之間的通訊發生錯誤。

   第二個步驟會嘗試以靜默方式交換Apple SSO設定檔，以取得Adobe驗證Token，以防萬一 **以上所有的都是false** 和 **以下所有情況均成立**:

   - 已為應用程式授予了用戶的TV Provider權限。
   - 用戶已在設備系統級別登錄到其TV Provider帳戶。
   - AccessEnabler iOS/tvOS SDK從視頻訂閱者帳戶框架中接收了用戶的電視提供者標識符。
   - 使用者與應用程式的電視提供者整合可透過Adobe Primetime TVE控制面板啟用。
   - 透過Adobe Primetime TVE控制面板，啟用使用者與應用程式的電視提供者單一登入。
   - 使用者的電視提供者未透過Adobe Primetime TVE控制面板降級。
   - AccessEnabler iOS/tvOS SDK從視訊訂閱者帳戶架構收到使用者的電視提供者SAML回應。

   **<u>專業提示：</u>** 此第二個步驟不會觸發任何其他回呼，除了 [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) 回呼，因為應用程式未明確啟動驗證。

1. 申請必須 [檢查驗證狀態](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **重要：** 第三步可能會觸發 [進階錯誤代碼](/help/authentication/error-reporting.md) 這是Apple SSO工作流程專屬的，若是 **以下其中一項是true**:

   - ***VSA403**  — 用戶在設備系統級別登錄到其TV Provider帳戶，但拒絕用戶對該應用程式的TV Provider權限。
   - ***VSA404**  — 用戶已在設備系統級別登錄到其TV Provider帳戶，但用戶的TV Provider權限未確定。
   - ***APPL\_ERROR**  — 用戶在設備系統級別登錄到其TV Provider帳戶，但AccessEnabler iOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。

   **重要：** 第三個步驟將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回呼 *狀態* 等於0，若為 **以下其中一項是true**:

   - 使用者未在裝置系統層級或透過一般驗證流程登入其電視提供者帳戶。
   - 使用者是透過裝置系統層級或一般驗證流程登入其TV Provider帳戶，但使用者的TV Provider驗證權杖TTL已通過。
   - 使用者是透過裝置系統層級或定期驗證流程登入其電視提供者帳戶，但使用者的電視提供者與應用程式的整合會透過Adobe Primetime TVE控制面板而停用。
   - 使用者是在裝置系統層級登入其電視提供者帳戶，但透過Adobe Primetime TVE控制面板，會停用使用者與應用程式的電視提供者單一登入。
   - 用戶在設備系統級別登錄到其TV Provider帳戶，但拒絕用戶對該應用程式的TV Provider權限。
   - 用戶已在設備系統級別登錄到其TV Provider帳戶，但用戶的TV Provider權限未確定。
   - 用戶在設備系統級別登錄到其TV Provider帳戶，但AccessEnabler iOS/tvOS SDK與視頻訂閱者帳戶框架之間的通信遇到錯誤。

   **重要：** 第三個步驟將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回呼 *狀態* 等於1，在 **以上所有內容均為false。**


1. 申請必須 [初始化驗證](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) 如果先前的驗證狀態檢查觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回呼 *狀態* 等於0。

   **<u>專業提示：</u>** 實作下列其中一項AccessEnabler iOS/tvOS SDK API [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) 或 [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **重要：** 第四步可能觸發 [進階錯誤代碼](/help/authentication/error-reporting.md) 這是Apple SSO工作流程專屬的，若是 **以下其中一項是true**:

   - ***VSA403***  — 拒絕用戶對應用程式的電視提供程式權限。
   - ***VSA404***  — 未確定應用程式的用戶的電視提供商權限。
   - ***VSA503*** - AccessEnabler iOS/tvOS SDK與視訊訂閱者帳戶架構之間的通訊發生錯誤。
   - ***N003***  — 使用者從Apple MVPD選擇器中選取「其他電視提供者」選項。
   - ***N004***  — 使用者從Apple MVPD選擇器中選取了電視提供者，目前要求者不支援（已停用整合或單一登入）。
   - ***N005***  — 使用者決定取消一般的MVPD選擇器或Apple MVPD選擇器。

   **重要：** 第四個步驟會借由觸發 [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) 回呼與 **one** 的 [高級錯誤代碼](/help/authentication/error-reporting.md)，在 **上述其中一個是真的**. 

   **重要：** 第四個步驟會借由觸發 [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) 或 [navigateToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) 回呼與 **無** 的 [高級錯誤代碼](/help/authentication/error-reporting.md)，若使用者選取不支援Apple SSO，但存在於Apple MVPD選取器中的電視提供者。

   **<u>專業提示：</u>** AccessEnabler iOS/tvOS SDK會自動呼叫 [setSelectedProvder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API，若使用者選取了不支援Apple SSO、但存在於Apple MVPD選擇器的電視提供者。

   **重要：** 第四個步驟會嘗試以靜默方式交換Apple SSO設定檔，以取得Adobe驗證Token，以防萬一 **以上所有的都是false** 和 **以下所有情況均成立**:

   - 已為應用程式授予了用戶的TV Provider權限。
   - 用戶已在設備系統級別登錄/當前登錄到其TV Provider帳戶。
   - AccessEnabler iOS/tvOS SDK從視頻訂閱者帳戶框架中接收了用戶的電視提供者標識符。
   - 使用者與應用程式的電視提供者整合可透過Adobe Primetime TVE控制面板啟用。
   - 透過Adobe Primetime TVE控制面板，啟用使用者與應用程式的電視提供者單一登入。
   - 使用者的電視提供者未透過Adobe Primetime TVE控制面板降級。
   - AccessEnabler iOS/tvOS SDK從視訊訂閱者帳戶架構收到使用者的電視提供者SAML回應。


 

>**<u>專業提示：</u>** 第四步將觸發 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) 回呼，無論 *狀態* 結果，因為驗證是由應用程式顯式啟動的。


</br>

### 中繼資料 {#Metadata}

應用程式可以選擇使用「*tokenSource」* [使用者中繼資料](/help/authentication/iostvos-sdk-api-reference.md#getMeta) 來自AccessEnabler iOS/tvOS SDK的API。

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### 登出 {#Logout}

此 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) framework不提供以程式設計方式登出已在裝置系統層級登入其電視提供者帳戶的人員的API。 因此，若要登出完全生效，一般使用者必須明確登出 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。 使用者必須擁有的另一個選項是從特定應用程式設定區段（電視提供者權限存取）撤回存取使用者訂閱資訊的權限。

>[!TIP]
>
> **<u>提示：</u>** 透過AccessEnabler iOS/tvOS SDK的媒體實作 [註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) API。


>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟執行tvOS實作。

- 申請必須 [啟動註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) 從AccessEnabler iOS/tvOS SDK。 這無法協助MVPD端的工作階段清除。
- 應用程式必須指示/提示使用者明確登出 *`Settings -> Accounts -> TV Provider`* 在tvOS上 [*VSA203* 狀態代碼已觸發](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟操作iOS/iPadOS實作。

- 申請必須 [啟動註銷](/help/authentication/iostvos-sdk-api-reference.md#logout) 從AccessEnabler iOS/tvOS SDK。 這有助於MVPD端的工作階段清除。
- 應用程式必須指示/提示使用者明確登出 *`Settings -> TV Provider`* 在iOS/iPadOS上，僅限在 [*VSA203* 狀態代碼已觸發](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
