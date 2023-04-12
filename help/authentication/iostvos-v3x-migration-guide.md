---
title: iOS/tvOS v3.x移轉指南
description: iOS/tvOS v3.x移轉指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# iOS/tvOS v3.x移轉指南 {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

>[!TIP]
> 
> **附註：**
>
> - 從iOS sdk 3.1版開始，實作人員現在可以交互使用WKWebView或UIWebView。 由於UIWebView已遭取代，因此應用程式應移轉至WKWebView，以避免未來iOS版本的問題。
> - 請注意，遷移只意味著使用WKWebView切換UIWebView類，對於Adobe的AccessEnabler ，沒有具體工作要做。


</br>

## 更新組建設定 {#update}

此版本包含以SWIFT語言編寫的功能。 如果您的應用程式完全是Objective-C，則需要將目標的構建設定中的「始終嵌入Swift標準庫」複選框設定為「是」。 設定此選項後，Xcode會掃描您應用程式中的套件架構，如果其中任何一個包含Swift程式碼，則會將相關程式庫複製到您應用程式的套件中。 如果您未更新生成設定，則您的應用程式可能會因錯誤而崩潰，指出它無法載入AccessEnabler.framework或各種 `ibswift*` 程式庫。

</br>

## 添加軟體語句 {#add}

> 有關如何獲取軟體聲明的資訊，請轉至此
> 頁面：
> [申請註冊](/help/authentication/iostvos-application-registration.md)

在您擁有軟體陳述式後，建議您將其托管在遠端伺服器上，這樣您就可以輕鬆撤銷或變更它，而無須在App Store中部署新版應用程式。 當應用程式啟動時，從遠程位置獲取您的軟體語句，並將其傳入AccessEnabler建構子中：

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> API資訊： [iOS / tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 新增自訂URL配置 {#add-custom}

> 如需如何取得自訂URL配置的相關資訊，請前往本頁： [取得客戶URL配置](/help/authentication/iostvos-application-registration.md)

取得自訂URL配置後，您需要將其新增至應用程式的info.plist檔案。 自訂配置具有以下格式： `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. 將冒號和正斜線新增至檔案時，您需要忽略它。 上述範例將變成 `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

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

## 在自訂URL配置上攔截呼叫 {#intercept}

這僅適用於應用程式以前通過 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) 針對需要Safari View Controller(SVC)的特定MVPD呼叫和，因此需要由SFSafariViewController控制器載入驗證和註銷端點的URL，而不是由UIWebView/WKWebView控制器。

在驗證和註銷流程期間，您的應用程式必須監控 `SFSafariViewController `控制器，因為它經過數個重新導向。 您的應用程式必須偵測載入您所定義之特定自訂URL的時機 `application's custom URL scheme` (例如`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. 當控制器載入此特定自訂URL時，您的應用程式必須關閉 `SFSafariViewController` 並調用AccessEnabler的 `handleExternalURL:url `API方法。

在 `AppDelegate` 新增下列方法：

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> API資訊： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 更新setRequestor方法簽名 {#update-setreq}

由於新的SDK使用新的驗證機制，因此不需要signedRequestId參數或公開金鑰和密碼（適用於tvOS）。 此 `setRequestor` 方法已簡化，而且只需requestorID即可。

### iOS

此程式碼：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

變成：

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

此程式碼：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

變成：

```swift
    accessEnabler.setRequestor(requestorId)
```

> API資訊： [設定請求者](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 將getAuthenticationToken方法取代為handleExternalURL方法 {#replace}

`getAuthentication` 方法過去用於完成驗證流程。 由於名稱有誤導性，因此重新命名為 `handleExternalURL` 並將url當作參數。

更改以下所有情況：

```swift
    accessEnabler.getAuthenticationToken()
```

進入這個：

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> API資訊： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)
