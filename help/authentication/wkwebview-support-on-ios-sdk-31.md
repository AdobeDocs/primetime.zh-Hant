---
title: iOSSDK 3.1+上的WKWebView支援
description: iOSSDK 3.1+上的WKWebView支援
exl-id: 90062be0-1a0a-44ae-8d8e-f4d97a92b17a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# iOSSDK 3.1+上的WKWebView支援 {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

**由於Apple棄用iOS上的UIWebView，我們更新了iOSSDK 3.1，支援WKWebView。**

## 相容性 {#compatibility}

從iOSSDK 3.1版開始，實施者現在可以互換使用WKWebView或UIWebView。 由於Apple已棄用UIWebView，因此應用應遷移到WKWebView，以避免將來的iOS版本出現問題。

請注意，遷移只需將UIWebView類與WKWebView切換即可，在Adobe的AccessEnabler方面沒有具體工作要做。

## 已知問題 {#known-issues}

Adobe的AccessEnabler使用隱藏的內部UIWebView實例執行「[被動認證](/help/authentication/sso-passive-authn.md)」的MVPD。 「被動」流對於需要對每個請求者ID進行身份驗證的MVPD非常有用，而來自此流的程式設計師在多個iOS應用程式中使用了相同的團隊ID以模擬SSO體驗(AdobeSSO)。 此功能當前由有限數量的MVPD使用。

該功能使用了UIWebView的行為，該行為允許Adobe捕獲驗證Cookie並在「被動」流期間重播它們。 WKWebView引入了更強的安全性，防止Adobe在登錄時捕獲Cookie集並使用WKWebView的隱藏實例重播它們。 由於這種安全性改進，並考慮到在非常具體的實施方案（多個應用程式使用相同的團隊ID）中，「被動」流只使一組非常有限的MVPD受益，Adobe刪除了使用webviews進行身份驗證的MVPD的「被動身份驗證」功能。

對於配置為使用SFSafariViewController的MVPD，該功能仍然存在，但請注意，在這種情況下，用戶將看到「被動」身份驗證，因為SFSafariViewController不能以「隱藏」方式使用。
