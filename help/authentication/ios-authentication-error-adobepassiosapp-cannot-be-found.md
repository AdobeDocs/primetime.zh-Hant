---
title: iOS驗證錯誤 — 找不到adobepass.ios.app
description: iOS驗證錯誤 — 找不到adobepass.ios.app
exl-id: cd97c6fb-f0fa-45c2-82c1-f28aa6b2fd12
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# iOS驗證錯誤 — 找不到adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## 問題 {#issue}

使用者正在執行驗證流程，當他們成功向提供者輸入認證後，系統會將他們重新導向回錯誤頁面、搜尋頁面或其他自訂頁面，通知他們 `adobepass.ios.app` 找不到/無法解析。

## 說明 {#explanation}

在iOS上， `adobepass.ios.app` 會作為最終重新導向URL使用，以指出AuthN流程已完成。 此時，應用程式需要向AccessEnabler提出要求，才能取得AuthN權杖及完成AuthN流程。

問題在於 `adobepass.ios.app` 實際上不存在，並且會在中觸發錯誤訊息 `webView`. 舊版iOS DemoApp假設此錯誤一律會在AuthN流程結束時觸發，並設定為據此處理(`indidFailLoadWithError`)。

**注意：** 此問題已在較新版本的DemoApp (隨iOS SDK下載提供)中修正。

很遺憾，此假設不正確。 有些所謂的「智慧」DNS或Proxy伺服器不會簡單地傳遞引發的錯誤，而是會執行下列其中一項作業： 

- 建立自訂錯誤頁面
- 轉寄至搜尋頁面或其他型別的客戶頁面或入口網站。

在這些情況下，回到iOS webView的回應在webView看來將是完全有效的回應，而且不會觸發舊DemoApp所依據的錯誤。

## 解決方案 {#solution}

請勿採取與DemoApp相同的假設。 改為在執行請求之前先擷取請求(在 `shouldStartLoadWithRequest`)並妥善處理。

如何在執行請求前截獲請求的範例：

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

請注意以下幾點：

- 永不使用 `adobepass.ios.app` 直接在程式碼中的任意位置存取。 請改用常數 `ADOBEPASS_REDIRECT_URL`
- 此 `return NO;` 陳述式將阻止頁面載入
- 請務必確認 `getAuthenticationToken` 呼叫在程式碼中只會呼叫一次。 多次呼叫目標 `getAuthenticationToken` 將導致未定義的結果。
