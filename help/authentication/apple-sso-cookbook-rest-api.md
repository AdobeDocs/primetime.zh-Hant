---
title: AppleSSO Cookbook(REST API)
description: AppleSSO Cookbook(REST API)
exl-id: cb27c4b7-bdb4-44a3-8f84-c522a953426f
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---

# AppleSSO Cookbook(REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 導言 {#Introduction}

Adobe Primetime認證REST API可支援平台單點登錄(SSO)認證，通過我們稱為AppleSSO工作流，為在iOS、iPadOS或tvOS上運行的客戶端應用程式的最終用戶提供此認證。

請注意，此文檔用作現有REST API文檔的擴展，可以找到 [這裡](/help/authentication/rest-api-reference.md)。

</br>

## 烹飪書 {#Cookbooks}

為了從AppleSSO用戶體驗中獲益，一個應用程式需要整合 [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框架，而Apple在與Adobe Primetime驗證REST API通信時，則必須遵循下面介紹的提示順序。

</br>

### 驗證 {#Authentication}

- [是否有有效的Adobe驗證令牌？](#Is_there_a_valid_Adobe_authentication_token)
- [用戶是否通過平台SSO登錄？](#Is_the_user_logged_in_via_Platform_SSO)
- [提取Adobe配置](#Fetch_Adobe_configuration)
- [使用Adobe配置啟動平台SSO工作流](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [用戶登錄是否成功？](#Is_user_login_successful)
- [從Adobe獲取所選MVPD的配置檔案請求](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [將Adobe請求轉發到平台SSO以獲取配置檔案](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [為Adobe驗證令牌交換平台SSO配置檔案](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [是否已成功生成Adobe令牌？](#Is_Adobe_token_generated_successfully)
- [啟動第二個螢幕身份驗證工作流](#Initiate_second_screen_authentication_workflow)
- [繼續授權流](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### 步驟：&quot;是否有有效的Adobe身份驗證令牌？&quot; {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 通過以下介質執行此操作： [Adobe Primetime驗證](/help/authentication/check-authentication-token.md) 服務。

</br>

#### 步驟：「用戶是否已通過平台SSO登錄？」 {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>提示：</u>** 通過以下介質執行此操作： [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框。

- 申請人必須檢查 [訪問權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶的訂閱資訊，並僅在用戶允許時繼續。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) 訂閱者帳戶資訊。
- 應用程式必須等待並處理 [元資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 的下界。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請遵循代碼段並特別注意注釋。

```swift
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

</br>

#### 步驟：&quot;獲取Adobe配置&quot; {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>提示：</u>** 通過以下介質執行此操作： [Adobe Primetime驗證](/help/authentication/provide-mvpd-list.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請注意MVPD屬性： *`enablePlatformServices`*。 *`boardingStatus`*。 *`displayInPlatformPicker`*。 *`platformMappingId`*。 *`requiredMetadataFields`* 注意其他步驟的代碼片段中的注釋。

</br>

#### 步驟「使用Adobe配置啟動平台SSO工作流」 {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>提示：</u>** 通過以下介質執行此操作： [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框。

- 申請人必須檢查 [訪問權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶的訂閱資訊，並僅在用戶允許時繼續。
- 該申請必須提供 [委託](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) VSAccountManager。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) 訂閱者帳戶資訊。
- 應用程式必須等待並處理 [元資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 的下界。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請遵循代碼段並特別注意注釋。


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### 步驟：&quot;用戶登錄是否成功？&quot; {#Is_user_login_successful}

>[!TIP]
>
> **<u>專業提示：</u>** 請注意中的代碼段 [&quot;使用Adobe配置啟動平台SSO工作流&quot;](#Initiate_Platform_SSO_workflow_with_Adobe_config) 的子菜單。 用戶登錄成功，以防 *`vsaMetadata!.accountProviderIdentifier`* 包含有效值，且當前日期尚未傳遞 *`vsaMetadata!.authenticationExpirationDate`* 值。

</br>

#### 步驟&quot;從Adobe獲取所選MVPD的配置檔案請求&quot; {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>提示：</u>** 通過Adobe Primetime身份驗證介質實現此功能 [配置檔案請求](/help/authentication/retrieve-profilerequest.md) 服務。

>[!TIP]
>
> **<u>專業提示：</u>** 請注意，從視頻訂閱者帳戶框架獲取的提供程式標識符表示 *`platformMappingId`* Adobe Primetime驗證配置。 因此，應用程式必須使用 *`platformMappingId`* 值，通過Adobe Primetime驗證 [提供MVPD清單](/help/authentication/provide-mvpd-list.md) 服務。

</br>

#### 步驟：&quot;將Adobe請求轉發到Platform SSO以獲取配置檔案&quot; {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>提示：</u>** 通過以下介質執行此操作： [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框。


- 申請人必須檢查 [訪問權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用戶的訂閱資訊，並僅在用戶允許時繼續。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) 訂閱者帳戶資訊。
- 應用程式必須等待並處理 [元資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 的下界。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請遵循代碼段並特別注意注釋。

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Primetime Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### 步驟：&quot;為Adobe驗證令牌交換平台SSO配置檔案&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 通過Adobe Primetime身份驗證介質實現此功能 [令牌交換](/help/authentication/token-exchange.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請注意中的代碼段 [&quot;將Adobe請求轉發到Platform SSO以獲取配置檔案&quot;](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) 的子菜單。 此 *`vsaMetadata!.samlAttributeQueryResponse!`* 表示 *`SAMLResponse`*，需要傳遞 [令牌交換](/help/authentication/token-exchange.md) 需要字串操作和編碼(*基64* 編碼 *URL* 之後編碼)。

</br>

#### 步驟：&quot;Adobe令牌是否生成成功？&quot; {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>提示：</u>** 通過媒體Adobe Primetime身份驗證實現此功能 [令牌交換](/help/authentication/token-exchange.md) 成功響應，這將是 *`204 No Content`*，表示已成功建立令牌並準備用於授權流。

</br>

#### 步驟：&quot;啟動第二個螢幕身份驗證工作流&quot; {#Initiate_second_screen_authentication_workflow}

**重要提示：** 「第二屏驗證工作流」術語適用於AppleTV，而「第一屏驗證工作流」/「常規驗證工作流」術語則更適用於iPhone和iPad。


>[!TIP]
>
> **<u>提示：</u>** 通過Adobe Primetime身份驗證介質實現此功能

[註冊代碼請求](/help/authentication/registration-code-request.md)。 [啟動身份驗證](/help/authentication/initiate-authentication.md) 和 [REST API檢索身份驗證令牌](/help/authentication/retrieve-authentication-token.md) 或 [檢查驗證令牌](/help/authentication/check-authentication-token.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請按照以下步驟執行tvOS實施。

- 申請必須 [獲取註冊代碼](/help/authentication/registration-code-request.md) 並在第1個設備（螢幕）上向最終用戶演示。
- 應用程式必須啟動 [輪詢以確認身份驗證狀態](/help/authentication/retrieve-authentication-token.md) 在獲得註冊碼後的第1裝置（螢幕）上。
- 另一個應用程式必須 [啟動驗證](/help/authentication/initiate-authentication.md) 當使用註冊碼時，在第2設備（螢幕）上。
- 應用程式必須停止 [輪詢](/help/authentication/retrieve-authentication-token.md) 第1設備（螢幕）上。

 

>[!TIP]
>
> **<u>專業提示：</u>** 按照以下步驟執行iOS/iPadOS實施。

- 申請必須 [獲取註冊代碼](/help/authentication/registration-code-request.md) 不應在第1個設備（螢幕）上向最終用戶顯示。
- 申請必須 [啟動驗證](/help/authentication/initiate-authentication.md) 使用註冊碼和 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件。
- 應用程式必須啟動 [輪詢以瞭解身份驗證狀態](/help/authentication/retrieve-authentication-token.md) 在 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件關閉。
- 應用程式必須停止 [輪詢](/help/authentication/retrieve-authentication-token.md) 第1設備（螢幕）上。

</br>

#### 步驟：&quot;繼續授權流&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>提示：</u>** 通過Adobe Primetime身份驗證介質實現此功能 [啟動授權](/help/authentication/initiate-authorization.md) 和 [獲取短媒體令牌](/help/authentication/obtain-short-media-token.md) 服務。

</br>

### 註銷 {#Logout}

的 [視頻訂戶帳戶](https://developer.apple.com/documentation/videosubscriberaccount) framework不提供API以寫程式方式註銷在設備系統級別登錄到其電視提供商帳戶的人員。 因此，要使註銷完全生效，最終用戶必須明確註銷 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上。 用戶需要的另一個選項是撤消從特定應用程式設定部分（電視提供程式訪問）訪問用戶訂閱資訊的權限。

>[!TIP]
>
> **<u>提示：</u>** 通過Adobe Primetime身份驗證介質實現此功能 [用戶元資料調用](/help/authentication/user-metadata.md) 和 [註銷](/help/authentication/initiate-logout.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請按照以下步驟執行tvOS實施。
 

- 應用程式必須使用「 」來確定是否由於通過平台SSO登錄而進行了身份驗證&#x200B;*tokenSource&quot;* [用戶元資料](/help/authentication/user-metadata.md) 從Adobe Primetime認證服務。
- 應用程式必須指示/提示用戶明確註銷 *`Settings -> Accounts -> TV Provider`* 在電視作業系統上 **僅** 以防 *&quot;令牌源&quot;* 值等於「*Apple」。*
- 申請必須 [啟動註銷](/help/authentication/initiate-logout.md) 使用直接HTTP調用從Adobe Primetime身份驗證服務獲取。 這無助於MVPD端的會話清理。

 

>[!TIP]
>
> **<u>專業提示：</u>** 按照以下步驟執行iOS/iPadOS實施。

- 應用程式必須使用「 」來確定是否由於通過平台SSO登錄而進行了身份驗證&#x200B;*tokenSource&quot;* [用戶元資料](/help/authentication/user-metadata.md) 從Adobe Primetime認證服務。
- 應用程式必須指示/提示用戶明確註銷 *`Settings -> TV Provider`* 在iOS/iPadOS上 **僅** 以防 *&quot;令牌源&quot;* 值等於 *&quot;Apple&quot;*。
- 申請必須 [啟動註銷](/help/authentication/initiate-logout.md) 從Adobe Primetime身份驗證服務 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件。 這將有助於在MVPD端進行會話清理。

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
