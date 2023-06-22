---
title: iOS/tvOS v3.x移轉指南
description: iOS/tvOS v3.x移轉指南
exl-id: 4c43013c-40af-48b7-af26-0bd7f8df2bdb
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# iOS/tvOS v3.x移轉指南 {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

>[!TIP]
> 
> **附註：**
>
> - 從iOS sdk 3.1版開始，實作者現在可以交換使用WKWebView或UIWebView。 由於UIWebView已過時，應用程式應移轉至WKWebView，以避免未來iOS版本發生問題。
> - 請注意，移轉僅表示使用WKWebView切換UIWebView類別，無需針對Adobe的AccessEnabler執行任何特定工作。


</br>

## 更新建置設定 {#update}

此版本包含以SWIFT語言撰寫的功能。 如果您的應用程式完全是Objective-C，則需要將target建置設定中的「一律內嵌Swift標準資料庫」核取方塊設為「是」。 設定此選項後，Xcode會掃描應用程式中的套件架構，如果其中任何一項包含Swift程式碼，則會將相關程式庫複製到應用程式的套件中。 如果您未更新組建設定，您的應用程式可能會當機並出現錯誤，指出它無法載入AccessEnabler.framework或 `ibswift*` 程式庫。

</br>

## 新增您的軟體宣告 {#add}

> 如需如何取得軟體宣告的詳細資訊，請前往此
> 頁面：
> [應用程式註冊](/help/authentication/iostvos-application-registration.md)

取得軟體陳述式後，建議您將其託管於遠端伺服器上，如此一來，只要在App Store中部署新版本的應用程式，即可輕鬆撤銷或變更陳述式。 當應用程式啟動時，請從遠端位置取得您的軟體陳述式，並將其傳遞到AccessEnabler建構函式：

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> API資訊在此： [iOS / tvOS API參考](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 新增自訂URL配置 {#add-custom}

> 如需如何取得自訂URL配置的相關資訊，請前往本頁面： [取得客戶URL配置](/help/authentication/iostvos-application-registration.md)

取得自訂URL配置後，您需要將其新增到應用程式的info.plist檔案中。 自訂配置具有此格式： `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. 將冒號和正斜線新增至檔案時，必須省略。 上述範例將變成 `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

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

## 攔截自訂URL配置上的呼叫 {#intercept}

唯有您的應用程式先前曾透過啟用手動Safari檢視控制器(SVC)處理時，此設定才適用。 [setoptions(\[&quot;handleSVC&quot;：true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) 針對需要Safari檢視控制器(SVC)的特定MVPD呼叫和，因此需要由SFSafariViewController而非UIWebView/WKWebView控制器載入驗證和登出端點的URL。

在驗證和登出流程期間，您的應用程式必須監控 `SFSafariViewController `控制器執行數個重新導向。 您的應用程式必須偵測載入由您定義的特定自訂URL的時刻。 `application's custom URL scheme` (例如：`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. 當控制器載入這個特定的自訂URL時，您的應用程式必須關閉 `SFSafariViewController` 並呼叫AccessEnabler的 `handleExternalURL:url `api方法。

在您的 `AppDelegate` 新增下列方法：

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> API資訊在此： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 更新setRequestor方法簽章 {#update-setreq}

由於新SDK使用新的驗證機制，因此不需要signedRequestId引數或公開金鑰和密碼（適用於tvOS）。 此 `setRequestor` 方法已簡化，只需要requestorID。

### iOS

此程式碼：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

會變成：

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

會變成：

```swift
    accessEnabler.setRequestor(requestorId)
```

> API資訊在此： [設定請求者](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 將getAuthenticationToken方法取代為handleExternalURL方法 {#replace}

`getAuthentication` 過去使用方法來完成驗證流程。 由於名稱有誤導性，因此將重新命名為 `handleExternalURL` 和會以url作為引數。

變更下列專案的所有具體值：

```swift
    accessEnabler.getAuthenticationToken()
```

變更為這個：

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> API資訊在此： [處理外部URL](/help/authentication/iostvos-sdk-api-reference.md)
