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
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 問題 {#issue}

用戶正在經歷驗證流，在他們成功輸入其提供商的憑據後，他們將被重定向回錯誤頁、搜索頁或某些其他自定義頁，通知他們 `adobepass.ios.app` 找不到/解決。

## 解釋 {#explanation}

在iOS, `adobepass.ios.app` 用作最終重定向URL以指示AuthN流已完成。 此時，應用需要向AccessEnabler發出請求，以獲取AuthN令牌並完成AuthN流。

問題是 `adobepass.ios.app` 實際上不存在，並將在 `webView`。 iOSDemoApp的較舊版本假定此錯誤將始終在AuthN流的末尾觸發，並設定為相應地處理該錯誤(`indidFailLoadWithError`)。

**注：** 此問題已在DemoApp的較新版本(隨iOSSDK下載一起提供)中解決。

不幸的是，這一假設並不正確。 有些所謂的「智慧」DNS或代理伺服器不會簡單地傳遞引發的錯誤，而會執行下列操作之一： 

- 建立自定義錯誤頁
- 轉發到搜索頁面，或某些其他類型的客戶頁面或門戶。

在這些情況下，返回到iOSWebView的響應對於WebView來說將是完全有效的響應，不會觸發舊DemoApp所依賴的錯誤。

## 解決方案 {#solution}

不要假設DemoApp與DemoApp相同。 相反，在請求執行之前攔截該請求(在 `shouldStartLoadWithRequest`)並妥善處理。

如何在請求執行之前攔截該請求的示例：

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

需要注意的幾點：

- 永不使用 `adobepass.ios.app` 直接在代碼的任何位置。 而是使用常數 `ADOBEPASS_REDIRECT_URL`
- 的 `return NO;` 語句將阻止載入頁面
- 確保 `getAuthenticationToken` 在您的代碼中，呼叫一次且只呼叫一次。 多個呼叫至 `getAuthenticationToken` 將生成未定義的結果。
