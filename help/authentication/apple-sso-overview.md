---
title: AppleSSO概述
description: AppleSSO概述
exl-id: 7cf47d01-a35a-4c85-b562-e5ebb6945693
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---

# AppleSSO概述 {#apple-sso-overview}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#Introduction}

Apple提供了一個API，允許人們在設備系統級別登錄到其電視提供商帳戶，從而消除了逐個應用進行身份驗證的需要。

因此，Apple和Adobe Primetime認證公司合作為iPhone,iPad和Apple電視擁有者在TV Everywhere生態系統中建立了單一登錄(SSO)平台用戶體驗。

為了從Apple設備上的單一登錄(SSO)用戶體驗中獲益，有一個必須完成的先決條件清單。

</br>

## 先決條件 {#Prerequisites}

必備項可適用於參與TVE業務的一個或多個實體，如程式設計師、MVPD、Adobe Primetime身份驗證或Apple。

</br>

### 程式設計師 {#Programmer}

為了從單一登錄(SSO)用戶體驗中獲益，一個程式設計師必須：

1. 至少使用Xcode版本8和iOS/電視OS版本10。

1. 擁有 [視頻訂戶單次登錄權利](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) 已配置到其Apple開發人員帳戶。 請與Apple聯繫以啟用 [視頻訂戶帳戶框架](https://developer.apple.com/documentation/videosubscriberaccount) 你Apple隊的身份證。

1. 通過以下方式為每個所需的整合(Channel x MVPD)和所需平台(iOS/電視OS)啟用單一登錄(YES) [Adobe PrimetimeTVE儀表板](https://console.auth.adobe.com/)。

1. 使用以下兩種解決方案之一整合AppleSSO工作流，由Adobe Primetime身份驗證團隊提供：

   - Adobe Primetime認證REST API可支援平台單一登錄(SSO)認證，用於在iOS,iPadOS或tvOS上運行的客戶端應用程式的最終用戶。 另請參閱 [AppleSSO Cookbook(REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)。

   - Adobe Primetime認證AccessEnableriOS/tvOS SDK可支援平台單一登錄(SSO)認證，用於在iOS、iPadOS或tvOS上運行的客戶端應用程式的最終用戶。 另請參閱 [AppleSSO Cookbook(iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)。

   - **<u>專業提示：</u>** 為了能夠訪問用戶的訂閱資訊，用戶必須授予應用程式權限才能繼續，類似於提供對設備的攝像頭或麥克風的訪問。 每個應用程式都必須請求此權限，設備將保存用戶的選擇。 請記住，用戶可以通過轉到應用程式設定（電視提供商權限訪問）或從 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。

   - **<u>專業提示：</u>** 我們建議在應用程式進入前台狀態時請求用戶的權限，但這只是建議，因為應用程式可以檢查 [訪問權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶的訂閱資訊在需要用戶身份驗證之前的任何時間點。 此外，AccessEnableriOS/tvOS SDK API將在需要時自動請求用戶的權限。

   - **<u>專業提示：</u>** 我們建議通過解釋單一登錄(SSO)用戶體驗的優點來激勵拒絕授予訪問訂閱資訊權限的用戶。 請記住，用戶可以通過轉到應用程式設定（電視提供商權限訪問）或從 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。

結果應與以下用戶流一起建立體驗，建議您在開始開發應用程式之前先進行咨詢：

- [iPhone/iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) 用戶流
- [Apple電視](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) 用戶流


>[!IMPORTANT]
>
> 當單點登錄功能為 **啟用** 用於iOS/電視OS **和** 在Apple **托管（支援）或機械臂** 來自AppleSSO工作流的驗證/註銷流將涉及Apple和Adobe Primetime驗證解決方案，而所有其他流（授權、預授權、元資料等） 將僅由Adobe Primetime認證服務。


>[!IMPORTANT]
>
> 當單點登錄功能為 **禁用** 用於iOS/電視OS **或** 在Apple **不載入（不支援）** MVPD驗證/註銷流程將從AppleSSO工作流回退到僅由Adobe Primetime驗證服務的常規工作流。


>[!IMPORTANT]
>
> AppleSSO工作流的一個主要收益是用一個螢幕驗證用戶流來表示的，當單一登錄功能為 **啟用** 對於電視作業系統 **和** 在Apple **已掛起（支援）** MVPD


### MVPD {#MVPD}

為了從單一登錄(SSO)用戶體驗中獲益，一個MVPD必須：

 

1. 加入Apple的SSO工作流，在Apple這邊。 請聯繫Apple，協助登機進程。
1. 提供能夠處理用戶登錄表單的JavaScript TVML應用程式。 請聯繫Apple以接收正確的文檔。
1. 提供一個字串值，表示在登機過程中由Apple分配的提供程式標識符。 請與Adobe Primetime身份驗證聯繫以執行配置更改。

</br>

## 常見問題 {#FAQ}

1. 如果AppleSSO工作流出現問題，使用AccessEnableriOS/tvOS SDK的應用程式是否能夠回退到常規身份驗證流？
   - 這是可能的，但需要對 [Adobe PrimetimeTVE儀表板](https://console.auth.adobe.com/)。 的 *啟用單次登錄* 必須設定為 *否* 用於所需的整合(Channel x MVPD)和所需的平台(iOS/電視OS)。
   - 應用程式只有在調用後才確認配置更改 [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API，以防其使用AccessEnableriOS/tvOS SDK。
1. 應用程式是否知道通過平台SSO在其他設備或其他應用程式上登錄而導致身份驗證何時發生？
   - 此資訊將不可用。
1. 應用程式是否知道通過同一設備上的平台SSO登錄而導致的身份驗證何時發生？ 
   - 此資訊作為用戶元資料鍵的一部分可用： *令牌源*，應返回字串值：Apple。
1. 如果用戶通過訪問 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 使用未與應用程式整合的MVPD在tvOS部分上？
   - 當用戶啟動應用程式時，用戶將不會通過AppleSSO工作流進行身份驗證。 因此，應用程式必須回退到常規身份驗證流並提供其自己的MVPD選取器。
1. 如果用戶通過訪問 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在TVOS部分上使用具有 *啟用單次登錄* 設定 *否* 的 [Adobe PrimetimeTVE儀表板](https://console.auth.adobe.com/) iOS/電視作業系統平台？
   - 當用戶啟動應用程式時，用戶將不會通過AppleSSO工作流進行身份驗證。 因此，應用程式必須回退到常規身份驗證流並提供其自己的MVPD選取器。
1. 如果用戶的MVPD未被Apple封裝（不支援），但存在於Apple選取器中，會發生什麼情況？
   - 當用戶啟動應用程式時，用戶將只通過AppleSSO工作流選擇MVPD，而不完成驗證流。 因此，應用程式必須回退到常規身份驗證流，但可以使用已選擇的MVPD。
1. 如果用戶的MVPD未被Apple封裝（不支援），會發生什麼情況？
   - 當用戶啟動應用程式時，用戶將通過AppleSSO工作流選擇「其他電視提供程式」選取器選項。 因此，應用程式必須回退到常規身份驗證流並提供其自己的MVPD選取器。
1. 如果用戶具有通過介質降級的MVPD，將發生什麼 [Adobe PrimetimeTVE儀表板](https://console.auth.adobe.com/)?
   - 當用戶啟動應用程式時，用戶將通過降級機制進行身份驗證，而不是通過AppleSSO工作流進行身份驗證。
   - 用戶的體驗應是無縫的，而應用程式將通過 *N010* 警告代碼，以防其使用AccessEnableriOS/tvOS SDK。
1. MVPD用戶ID在AppleSSO和非AppleSSO驗證流之間是否會更改？
   - 期望用戶ID不會更改，但需要為每個選定的提供程式驗證它。 
1. 驗證TTL是否有任何更改？
   - Adobe Primetime驗證將繼續尊重程式設計師與每個MVPD整合所需的TTL。
   - 當通過AppleSSO從一個程式設計師應用程式導航到另一個程式設計師應用程式時，第二個應用程式將具有其相應程式設計師x MVPD整合的TTL（它將不共用驗證的第一個應用程式的TTL）

|  | Adobe Primetime身份驗證TTL已過期 | Adobe Primetime驗證TTL有效 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple設備令牌TTL已過期** | 未驗證用戶（應顯示MVPD選取器） | 用戶已經過身份驗證，TTL是其Adobe Primetime身份驗證令牌的剩餘時間 |
| **Apple設備令牌TTL有效** | 用戶已通過靜默身份驗證，並獲得另一個Adobe Primetime身份驗證令牌，該令牌在TVE儀表板中指定TTL | 用戶已經過身份驗證，TTL是其Adobe Primetime身份驗證令牌的剩餘時間 |

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
