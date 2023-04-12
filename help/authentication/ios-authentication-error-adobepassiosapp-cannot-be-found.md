---
title: iOS驗證錯誤 — 找不到adobepass.ios.app
description: iOS驗證錯誤 — 找不到adobepass.ios.app
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# iOS驗證錯誤 — 找不到adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 問題 {#issue}

使用者正在進行驗證流程，當他們成功輸入其提供者的認證後，就會重新導向回錯誤頁面、搜尋頁面或其他自訂頁面，通知他們 `adobepass.ios.app` 找不到/解決。

## 說明 {#explanation}

在iOS, `adobepass.ios.app` 作為最終重新導向URL，以指出AuthN流程已完成。 此時，應用程式需要向AccessEnabler提出請求，以取得AuthN代號並完成AuthN流程。

問題是 `adobepass.ios.app` 實際上不存在，且會在 `webView`. 舊版iOS DemoApp假設此錯誤一律會在AuthN流程結束時觸發，且已設定以據以處理(`indidFailLoadWithError`)。

**注意：** 此問題已在舊版DemoApp中修正(隨附於iOS SDK下載)。

不幸的是，這一假設並不正確。 有些所謂的「智慧」DNS或Proxy伺服器不會只是傳遞引發的錯誤，而會執行下列其中一項作業： 

- 建立自訂錯誤頁面
- 轉送至搜尋頁面，或某些其他類型的客戶頁面或入口網站。

在這些情況下，回到iOS webView的回應就webView而言將是完全有效的回應，且不會觸發舊DemoApp所依賴的錯誤。

## 解決方案 {#solution}

請勿假設與DemoApp相同。 請改為在執行請求前加以截取(在 `shouldStartLoadWithRequest`)並妥善處理。

如何在執行請求之前截取請求的範例：

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

- 永不使用 `adobepass.ios.app` 直接放在程式碼中任何位置。 請改用常數 `ADOBEPASS_REDIRECT_URL`
- 此 `return NO;` 語句將阻止頁面載入
- 請務必確認 `getAuthenticationToken` 在您的程式碼中，呼叫一次，且只呼叫一次。 對進行多次呼叫 `getAuthenticationToken` 將導致未定義的結果。

