---
title: iOS SDK 3.1以上版本的WKWebView支援
description: iOS SDK 3.1以上版本的WKWebView支援
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# iOS SDK 3.1以上版本的WKWebView支援 {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

**由於Apple在iOS上淘汰UIWebView，我們已更新iOS SDK 3.1，並支援WKWebView。**

## 相容性 {#compatibility}

從iOS SDK 3.1版開始，實作者現在可以交互使用WKWebView或UIWebView。 由於Apple已棄用UIWebView，因此應用程式應移轉至WKWebView，以避免未來iOS版本的問題。

請注意，遷移只意味著使用WKWebView切換UIWebView類，對於Adobe的AccessEnabler ，沒有具體工作要做。

## 已知問題 {#known-issues}

Adobe的AccessEnabler使用隱藏的內部UIWebView實例執行「[被動認證](/help/authentication/sso-passive-authn.md)」（針對某些MVPD）。 「被動」流程對於需要驗證每個請求者ID的MVPD非常有用，而透過此流程，在多個iOS應用程式中使用相同團隊ID來模擬SSO體驗(AdobeSSO)的程式設計人員將受益匪淺。 目前有限數量的MVPD會使用此功能。

此功能使用UIWebView的行為，允許Adobe擷取驗證Cookie，並在「被動」流程期間重播。 WKWebView引入了更強的安全性，防止Adobe在登入時擷取Cookie集，並使用WKWebView的隱藏例項重播這些Cookie。 由於這項安全性改善，並考慮到在非常特定的實作案例（使用相同團隊ID的多個應用程式）中，「被動」流只使極有限的一組MVPD受益，因此，Adobe移除了使用webviews進行驗證的MVPD的「被動驗證」功能。

配置為使用SFSafariViewController的MVPD仍存在該功能，但請注意，在此情況下，用戶將看到「被動」身份驗證，因為SFSafariViewController不能以「隱藏」方式使用。
