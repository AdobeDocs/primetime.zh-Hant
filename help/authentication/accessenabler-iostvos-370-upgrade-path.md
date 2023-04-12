---
title: AccessEnabler iOS/tvOS 3.7.0升級路徑
description: AccessEnabler iOS/tvOS 3.7.0升級路徑
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# AccessEnabler iOS/tvOS 3.7.0升級路徑 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

</br>

鍵鏈儲存從 [新AccessEnabler 3.7.0版](/help/authentication/authn-rn-ios-tvos-370.md) 與AccessEnabler版本低於3.7.0的Keychain儲存實施不相容。

採用新AccessEnabler 3.7.0版的一個應用程式的升級路徑將遷移來自舊版鑰匙圈儲存的所有令牌。 因此，使用者 **不應丟失驗證/授權會話** 在AccessEnabler框架更新過程中。

## 已知限制

實施者可能會遇到一些限制（如下所述）。


1. 常規(Adobe)SSO在使用AccessEnabler 3.7.0版的一個應用程式和使用低於3.7.0版的AccessEnabler的一個應用程式之間將無法工作，即使是同一供應商開發的應用程式也是如此。

   - **重要：**
      - 系統層級(Apple)SSO不受影響！
      - 如果兩個應用程式是由同一供應商開發的，並且使用低於3.7.0的AccessEnabler版本，則常規(Adobe)SSO將繼續工作！
      - 如果兩個應用程式是由同一供應商開發的，並且使用AccessEnabler 3.7.0版，則常規(Adobe)SSO將有效！

1. 如果使用AccessEnabler 3.7.0版將一個應用程式降級到較低版本的AccessEnabler，則不會遷移新生成的令牌。 因此，最終用戶可能會遇到驗證/授權會話丟失的情況，而不是預期。

   - **重要：**
      - 透過系統層級(Apple)SSO驗證的一般使用者將不受影響！
      - 在使用AccessEnabler 3.7.0版更新到新應用程式之前已經驗證的最終用戶將不受影響！

1. 如果使用AccessEnabler 3.7.0版將一個應用程式降級到較低版本的AccessEnabler，則刪除的令牌將不會被確認。 因此，最終用戶可能會遇到驗證/授權會話的存在，而不期望它。
