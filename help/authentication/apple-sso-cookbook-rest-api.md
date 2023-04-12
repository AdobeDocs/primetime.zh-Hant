---
title: Apple SSO逐步指南(REST API)
description: Apple SSO逐步指南(REST API)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Apple SSO逐步指南(REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 簡介 {#Introduction}

Adobe Primetime驗證REST API可支援平台單一登入(SSO)驗證，適用於在iOS、iPadOS或tvOS上執行之用戶端應用程式的一般使用者，這需透過我們稱為Apple SSO工作流程。

請注意，本檔案是現有REST API檔案的擴充功能，請參閱 [此處](/help/authentication/rest-api-reference.md).

</br>

## 逐步指南 {#Cookbooks}

為了從Apple SSO使用者體驗中獲益，一個應用程式需要整合 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 由Apple開發的架構，雖然Adobe Primetime Authentication REST API通訊方面，但必須遵循下列提示順序。

</br>

### 驗證 {#Authentication}

- [是否有有效的Adobe驗證令牌？](#Is_there_a_valid_Adobe_authentication_token)
- [使用者是否透過Platform SSO登入？](#Is_the_user_logged_in_via_Platform_SSO)
- [擷取Adobe設定](#Fetch_Adobe_configuration)
- [使用Adobe設定啟動平台SSO工作流程](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [使用者登入是否成功？](#Is_user_login_successful)
- [從Adobe取得所選MVPD的設定檔請求](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [將Adobe要求轉送至Platform SSO以取得設定檔](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [為Adobe驗證Token交換Platform SSO設定檔](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [Adobe權杖是否成功產生？](#Is_Adobe_token_generated_successfully)
- [啟動第二螢幕驗證工作流](#Initiate_second_screen_authentication_workflow)
- [繼續執行授權流程](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### 步驟：&quot;是否有有效的Adobe驗證令牌？&quot; {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 透過以下媒體實作 [Adobe Primetime驗證](/help/authentication/check-authentication-token.md) 服務。

</br>

#### 步驟：「使用者是否透過Platform SSO登入？」 {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>提示：</u>** 透過以下媒體實作 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框架。

- 申請人必須檢查 [存取權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 使用者的訂閱資訊，並僅在使用者允許時才繼續。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解訂閱者帳戶資訊。
- 應用程式必須等待並處理 [中繼資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 資訊。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請依照程式碼片段操作，並額外注意註解。

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
> **<u>提示：</u>** 透過以下媒體實作 [Adobe Primetime驗證](/help/authentication/provide-mvpd-list.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請注意MVPD屬性： *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* 並特別注意程式碼片段中其他步驟的註解。

</br>

#### 步驟「使用Adobe設定啟動平台SSO工作流程」 {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>提示：</u>** 透過以下媒體實作 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框架。

- 申請人必須檢查 [存取權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 使用者的訂閱資訊，並僅在使用者允許時才繼續。
- 申請必須提供 [委派](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) VSAccountManager的。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解訂閱者帳戶資訊。
- 應用程式必須等待並處理 [中繼資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 資訊。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請依照程式碼片段操作，並額外注意註解。


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
> **<u>專業提示：</u>** 請注意 [&quot;使用Adobe配置啟動平台SSO工作流&quot;](#Initiate_Platform_SSO_workflow_with_Adobe_config) 步驟。 使用者登入成功，以防 *`vsaMetadata!.accountProviderIdentifier`* 包含有效值，且目前日期尚未傳遞 *`vsaMetadata!.authenticationExpirationDate`* 值。

</br>

#### 步驟&quot;從所選MVPD的Adobe取得設定檔要求&quot; {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>提示：</u>** 透過Adobe Primetime驗證的媒體實作 [設定檔請求](/help/authentication/retrieve-profilerequest.md) 服務。

>[!TIP]
>
> **<u>專業提示：</u>** 請注意，從視訊訂閱者帳戶架構取得的提供者識別碼代表 *`platformMappingId`* Adobe Primetime驗證設定。 因此，應用程式必須使用 *`platformMappingId`* 值，透過Adobe Primetime驗證的媒體 [提供MVPD清單](/help/authentication/provide-mvpd-list.md) 服務。

</br>

#### 步驟：&quot;將Adobe要求轉送至Platform SSO以取得設定檔&quot; {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>提示：</u>** 透過以下媒體實作 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) 框架。


- 申請人必須檢查 [存取權限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 使用者的訂閱資訊，並僅在使用者允許時才繼續。
- 申請書必須提交 [請求](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) ，以了解訂閱者帳戶資訊。
- 應用程式必須等待並處理 [中繼資料](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) 資訊。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請依照程式碼片段操作，並額外注意註解。

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

#### 步驟：&quot;為Adobe驗證Token交換平台SSO設定檔&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>提示：</u>** 透過Adobe Primetime驗證的媒體實作 [代號交換](/help/authentication/token-exchange.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請注意 [&quot;將Adobe要求轉送至Platform SSO以取得設定檔&quot;](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) 步驟。 此 *`vsaMetadata!.samlAttributeQueryResponse!`* 代表 *`SAMLResponse`*，需要傳遞 [代號交換](/help/authentication/token-exchange.md) 和需要字串操作和編碼(*Base64* 編碼 *URL* 之後進行編碼)。

</br>

#### 步驟：&quot;Adobe令牌是否生成成功？&quot; {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>提示：</u>** 透過媒體Adobe Primetime驗證實作 [代號交換](/help/authentication/token-exchange.md) 成功的回應， *`204 No Content`*，表示已成功建立代號，且已準備好用於授權流程。

</br>

#### 步驟：&quot;啟動第二螢幕驗證工作流&quot; {#Initiate_second_screen_authentication_workflow}

**重要：** 「第二螢幕驗證工作流程」術語適用於AppleTV，而「第一螢幕驗證工作流程」/「一般驗證工作流程」術語則更適用於iPhone和iPad。


>[!TIP]
>
> **<u>提示：</u>** 透過Adobe Primetime驗證的媒體實作

[註冊代碼請求](/help/authentication/registration-code-request.md), [啟動驗證](/help/authentication/initiate-authentication.md) 和 [REST API擷取驗證Token](/help/authentication/retrieve-authentication-token.md) 或 [檢查驗證Token](/help/authentication/check-authentication-token.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟執行tvOS實作。

- 申請必須 [取得註冊碼](/help/authentication/registration-code-request.md) 並在第1部裝置（畫面）上向使用者呈現。
- 申請必須開始 [輪詢以確認身份驗證狀態](/help/authentication/retrieve-authentication-token.md) 在獲得註冊碼後的第1裝置（螢幕）上。
- 另一個申請必須 [啟動驗證](/help/authentication/initiate-authentication.md) 在第2個裝置（畫面）上使用註冊代碼時。
- 申請必須停止 [輪詢](/help/authentication/retrieve-authentication-token.md) 在產生驗證權杖時的第一個裝置（畫面）上。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟操作iOS/iPadOS實作。

- 申請必須 [取得註冊碼](/help/authentication/registration-code-request.md) 不應在第1部裝置（畫面）上向使用者呈現。
- 申請必須 [啟動驗證](/help/authentication/initiate-authentication.md) 在第1個裝置（畫面）上使用註冊碼和 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件。
- 申請必須開始 [輪詢以了解驗證狀態](/help/authentication/retrieve-authentication-token.md) 在 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件關閉。
- 申請必須停止 [輪詢](/help/authentication/retrieve-authentication-token.md) 在產生驗證權杖時的第一個裝置（畫面）上。

</br>

#### 步驟：&quot;繼續執行授權流程&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>提示：</u>** 透過Adobe Primetime驗證的媒體實作 [啟動授權](/help/authentication/initiate-authorization.md) 和 [取得短媒體代號](/help/authentication/obtain-short-media-token.md) 服務。

</br>

### 登出 {#Logout}

此 [視訊訂閱者帳戶](https://developer.apple.com/documentation/videosubscriberaccount) framework不提供以程式設計方式登出已在裝置系統層級登入其電視提供者帳戶的人員的API。 因此，若要登出完全生效，一般使用者必須明確登出 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。 使用者必須擁有的另一個選項是從特定應用程式設定區段（電視提供者存取）撤回存取使用者訂閱資訊的權限。

>[!TIP]
>
> **<u>提示：</u>** 透過Adobe Primetime驗證的媒體實作 [使用者中繼資料呼叫](/help/authentication/user-metadata.md) 和 [登出](/help/authentication/initiate-logout.md) 服務。


>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟執行tvOS實作。
 

- 應用程式必須判斷驗證是否因透過平台SSO登入而發生，使用「*tokenSource」* [使用者中繼資料](/help/authentication/user-metadata.md) 從Adobe Primetime驗證服務。
- 應用程式必須指示/提示使用者明確登出 *`Settings -> Accounts -> TV Provider`* 在tvOS上 **僅限** 在 *&quot;tokenSource&quot;* 值等於「*Apple」。*
- 申請必須 [啟動註銷](/help/authentication/initiate-logout.md) 來驗證Adobe Primetime。 這無法協助MVPD端的工作階段清除。

 

>[!TIP]
>
> **<u>專業提示：</u>** 請依照下列步驟操作iOS/iPadOS實作。

- 應用程式必須判斷驗證是否因透過平台SSO登入而發生，使用「*tokenSource」* [使用者中繼資料](/help/authentication/user-metadata.md) 從Adobe Primetime驗證服務。
- 應用程式必須指示/提示使用者明確登出 *`Settings -> TV Provider`* 在iOS/iPadOS上 **僅限** 在 *&quot;tokenSource&quot;* 值等於 *&quot;Apple&quot;*.
- 申請必須 [啟動註銷](/help/authentication/initiate-logout.md) 來自Adobe Primetime驗證服務，使用 [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) 或 [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) 元件。 這有助於MVPD端的工作階段清除。

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->

