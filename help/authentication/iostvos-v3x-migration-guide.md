---
title: iOS/電視OS v3.x遷移指南
description: iOS/電視OS v3.x遷移指南
exl-id: 4c43013c-40af-48b7-af26-0bd7f8df2bdb
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# iOS/電視OS v3.x遷移指南 {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

>[!TIP]
> 
> **附註：**
>
> - 從iOSSDK 3.1版開始，實現程式現在可以互換使用WKWebView或UIWebView。 由於UIWebView已棄用，因此應用應遷移到WKWebView，以避免將來的iOS版本出現問題。
> - 請注意，遷移只需將UIWebView類與WKWebView切換即可，在Adobe的AccessEnabler方面沒有具體工作要做。


</br>

## 更新生成設定 {#update}

此版本包含以SWIFT語言編寫的功能。 如果您的應用完全為Objective-C，則需要將目標的生成設定中的「始終嵌入Swift標準庫」複選框設定為「是」。 設定此選項後，Xcode將掃描應用中捆綁的框架，如果其中任何框架包含Swift代碼，它會將相關庫複製到應用的捆綁包中。 如果您不更新生成設定，則您的應用可能會崩潰，出現錯誤，指出它無法載入AccessEnabler.framework或各種 `ibswift*` 庫。

</br>

## 添加軟體語句 {#add}

> 有關如何獲取軟體語句的資訊，請轉到此
> 頁：
> [申請註冊](/help/authentication/iostvos-application-registration.md)

一旦您擁有了軟體語句，我們建議您將其托管在遠程伺服器上，這樣您就可以輕鬆撤銷或更改它，而無需在App Store部署新版本的應用程式。 當應用程式啟動時，從遠程位置獲取軟體語句並在AccessEnabler建構子中傳遞：

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> 此處為API資訊： [iOS/tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 添加自定義URL方案 {#add-custom}

> 有關如何獲取自定義URL方案的資訊，請轉至此頁： [獲取客戶URL方案](/help/authentication/iostvos-application-registration.md)

獲取自定義URL方案後，需要將其添加到應用程式的info.plist檔案中。 自定義方案具有以下格式： `adbe.u-XFXJeTSDuJiIQs0HVRAg://`。 將冒號和正斜槓添加到檔案時，需要忽略它。 上例將變成 `adbe.u-XFXJeTSDuJiIQs0HVRAg`。

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## 截取自定義URL方案的呼叫 {#intercept}

僅當應用程式以前通過以下方式啟用手動Safari View Controller(SVC)處理時，才適用 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) 調用和特定MVPD，需要Safari View Controller(SVC)，因此需要由SFSafariViewController控制器而不是UIWebView/WKWebView控制器載入驗證和註銷端點的URL。

在驗證和註銷流程期間，您的應用程式必須監視 `SFSafariViewController `控制器，因為它經過多個重定向。 應用程式必須檢測載入由您定義的特定自定義URL的時間 `application's custom URL scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`。 當控制器載入此特定自定義URL時，您的應用程式必須關閉 `SFSafariViewController` 並調用AccessEnabler `handleExternalURL:url `API方法。

在 `AppDelegate` 添加以下方法：

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> 此處為API資訊： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 更新setRequestor方法簽名 {#update-setreq}

由於新SDK使用新的身份驗證機制，因此不需要signedRequestId參數或公鑰和密鑰（對於tvOS）。 的 `setRequestor` 方法簡化，只需請求者ID。

### iOS

此代碼：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

變為：

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### 電視作業系統

此代碼：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

變為：

```swift
    accessEnabler.setRequestor(requestorId)
```

> 此處為API資訊： [設定請求者](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 將getAuthenticationToken方法替換為handleExternalURL方法 {#replace}

`getAuthentication` 過去採用方法完成認證流程。 因為名字有誤導性，所以改名為 `handleExternalURL` 並將url作為參數。

更改此項的所有實例：

```swift
    accessEnabler.getAuthenticationToken()
```

到此：

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> 此處為API資訊： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)
