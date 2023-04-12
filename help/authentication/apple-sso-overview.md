---
title: Apple SSO概述
description: Apple SSO概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Apple SSO概述 {#apple-sso-overview}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#Introduction}

Apple提供API，可讓使用者在裝置系統層級登入其電視提供者帳戶，不需依應用程式進行驗證。

因此，Apple和Adobe Primetime Authentication合作，針對iPhone、iPad和Apple TV擁有者，在TV Everywhere生態系統中建立平台單一登入(SSO)使用者體驗。

為了從Apple裝置上的單一登入(SSO)使用者體驗中受益，必須填寫先決條件清單。

</br>

## 必要條件 {#Prerequisites}

先決條件可適用於參與TVE業務的一或多個實體，例如程式設計師、MVPD、Adobe Primetime驗證或Apple。

</br>

### 程式設計師 {#Programmer}

為了從單一登錄(SSO)用戶體驗中受益，一個程式設計師必須：

1. 請至少使用Xcode 8版和iOS/tvOS 10版。

1. 擁有 [視頻訂閱者單一登錄權限](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) 設為其Apple開發人員帳戶。 請連絡Apple以啟用 [視訊訂閱者帳戶架構](https://developer.apple.com/documentation/videosubscriberaccount) 以取得Apple團隊ID。

1. 透過，針對每個需要的整合(Channel x MVPD)和所需平台(iOS / tvOS)啟用單一登入(YES) [Adobe Primetime TVE儀表板](https://console.auth.adobe.com/).

1. 使用Adobe Primetime驗證團隊提供的下列兩個解決方案之一，整合Apple SSO工作流程：

   - Adobe Primetime驗證REST API可支援適用於在iOS、iPadOS或tvOS上執行之用戶端應用程式的一般使用者的平台單一登入(SSO)驗證。 另請參閱 [Apple SSO逐步指南(REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可支援平台單一登入(SSO)驗證，適用於iOS、iPadOS或tvOS上執行之用戶端應用程式的一般使用者。 另請參閱 [Apple SSO逐步指南(iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>專業提示：</u>** 為了能夠訪問用戶的訂閱資訊，用戶必須授予應用程式繼續的權限，類似於提供對設備的攝像頭或麥克風的訪問。 必須按應用程式請求此權限，設備將保存用戶的選擇。 請記住，使用者可以前往應用程式設定（電視提供者權限存取）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

   - **<u>專業提示：</u>** 我們建議在應用程式進入前景狀態時請求使用者的權限，但這只是建議，因為應用程式可以檢查 [存取權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶在需要用戶驗證之前的任何時間點的訂閱資訊。 此外， AccessEnabler iOS/tvOS SDK API將在需要時自動請求用戶的權限。

   - **<u>專業提示：</u>** 建議您說明單一登入(SSO)使用者體驗的優點，以鼓勵拒絕授予存取訂閱資訊權限的使用者。 請記住，使用者可以前往應用程式設定（電視提供者權限存取）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

結果應會建立符合下列使用者流程的體驗，建議您在開始開發應用程式之前先諮詢這些流程：

- [iPhone/iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) 使用者流程
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) 使用者流程


>[!IMPORTANT]
>
> 單一登入功能為 **已啟用** 適用於iOS/tvOS **和** 在Apple **已上線（支援）或選擇器** 來自Apple SSO工作流程的驗證/登出流程將同時涉及Apple和Adobe Primetime驗證解決方案，而所有其他流程（授權、預先授權、中繼資料等） 將僅由Adobe Primetime驗證服務。


>[!IMPORTANT]
>
> 單一登入功能為 **停用** 適用於iOS/tvOS **或** 在Apple **未上線（不支援）** 驗證/登出流程將從Apple SSO工作流程退回至僅由Adobe Primetime驗證服務的一般工作流程。


>[!IMPORTANT]
>
> Apple SSO工作流程的主要優點之一，是以單一螢幕驗證使用者流程來呈現，當單一登入功能為 **已啟用** tvOS適用 **和** 在Apple **已上線（支援）** MVPD。


### MVPD {#MVPD}

為了從單一登入(SSO)使用者體驗中獲益，一個MVPD必須：

 

1. 在Apple端上線至Apple SSO工作流程。 請聯絡Apple以加速上線程式。
1. 提供可處理使用者登入表單的JavaScript TVML應用程式。 請聯絡Apple以取得適當檔案。
1. 提供字串值，代表Apple在上線程式期間指派的提供者識別碼。 請聯絡Adobe Primetime驗證以執行設定變更。

</br>

## 常見問題集 {#FAQ}

1. 如果Apple SSO工作流程發生問題，使用AccessEnabler iOS/tvOS SDK的應用程式是否能後援至一般驗證流程？
   - 這是可能的，但需要對 [Adobe Primetime TVE儀表板](https://console.auth.adobe.com/). 此 *啟用單一登入* 必須設定在 *否* 以取得所需的整合(Channel x MVPD)和所需平台(iOS/tvOS)。
   - 應用程式只有在呼叫 [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API(若使用的是AccessEnabler iOS/tvOS SDK)。
1. 應用程式是否會知道何時由於通過平台SSO在其他設備或其他應用程式上登錄而發生了身份驗證？
   - 此資訊將不可用。
1. 應用程式是否會知道何時由於在同一設備上通過平台SSO登錄而發生驗證？ 
   - 此資訊屬於使用者中繼資料索引鍵的一部分： *tokenSource*，應會傳回字串值：「Apple」。
1. 如果使用者透過前往 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 使用未與應用程式整合的MVPD時，在tvOS區段上取得Adobe Cloud ID和Analytics ID?
   - 當使用者啟動應用程式時，不會透過Apple SSO工作流程驗證使用者。 因此，應用程式必須回退至一般驗證流程，並提供其自己的MVPD選擇器。
1. 如果使用者透過前往 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS區段上，使用具有 *啟用單一登入* 設定於 *否* 在 [Adobe Primetime TVE儀表板](https://console.auth.adobe.com/) iOS/tvOS平台？
   - 當使用者啟動應用程式時，不會透過Apple SSO工作流程驗證使用者。 因此，應用程式必須回退至一般驗證流程，並提供其自己的MVPD選擇器。
1. 如果使用者的MVPD未由Apple上線（不支援），但存在於Apple選擇器中，會發生什麼事？
   - 當使用者啟動應用程式時，使用者只會透過Apple SSO工作流程選取MVPD，而不會完成驗證流程。 因此，應用程式必須退回一般驗證流程，但可能會使用已選取的MVPD。
1. 如果使用者的MVPD未上線（不支援）,Apple會發生什麼事？
   - 當使用者啟動應用程式時，使用者會透過Apple SSO工作流程選取「其他電視提供者」選擇器選項。 因此，應用程式必須回退至一般驗證流程，並提供其自己的MVPD選擇器。
1. 如果使用者的MVPD透過 [Adobe Primetime TVE儀表板](https://console.auth.adobe.com/)?
   - 當使用者啟動應用程式時，將會透過降級機制驗證使用者，而非透過Apple SSO工作流程。
   - 使用者的體驗應會順暢無礙，而應用程式則會透過 *N010* 警告代碼，以防其使用AccessEnabler iOS/tvOS SDK。
1. Apple SSO和非Apple SSO驗證流程之間的MVPD使用者ID是否會變更？
   - 期望是使用者ID不會變更，但需要為每個選取的提供者驗證。 
1. 驗證TTL是否會有任何變更？
   - Adobe Primetime驗證會持續遵循程式設計人員與每個MVPD整合所需的TTL。
   - 當通過Apple SSO從一個程式設計師應用程式導航到另一個程式設計師應用程式時，第二個應用程式將具有其相應程式設計師x MVPD整合的TTL（它不共用驗證的第一個應用程式的TTL）

|  | Adobe Primetime驗證TTL已過期 | Adobe Primetime驗證TTL有效 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple的裝置代號TTL已過期** | 使用者未驗證（應顯示MVPD選取器） | 使用者已驗證，而TTL是其Adobe Primetime驗證Token的剩餘時間 |
| **Apple的裝置代號TTL有效** | 使用者會自動通過驗證，並透過TVE Dashboard中指定的TTL取得另一個Adobe Primetime驗證Token | 使用者已驗證，而TTL是其Adobe Primetime驗證Token的剩餘時間 |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
