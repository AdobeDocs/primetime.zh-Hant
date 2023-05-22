---
title: AccessEnableriOS/tvOS 3.7.0升級路徑
description: AccessEnableriOS/tvOS 3.7.0升級路徑
exl-id: f15c7414-ec9b-4e21-b457-1ecf59f47441
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# AccessEnableriOS/tvOS 3.7.0升級路徑 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

</br>

鍵鏈儲存更改 [新的AccessEnabler 3.7.0版](/help/authentication/authn-rn-ios-tvos-370.md) 與AccessEnabler版本低於3.7.0的Keychain儲存實現不相容。

採用新AccessEnabler 3.7.0版的一個應用程式的升級路徑將遷移Keychain儲存以前版本的所有令牌。 因此，最終用戶 **不應丟失驗證/授權會話** 在AccessEnabler框架更新過程中。

## 已知限制

實施者可能會遇到一些限制，如下所述。


1. 常規(Adobe)SSO在使用AccessEnabler版本3.7.0的一個應用程式和使用低於3.7.0的AccessEnabler版本的一個應用程式之間無法工作，即使對於由同一供應商開發的應用程式也是如此。

   - **重要提示：**
      - 系統級(Apple)SSO將不受影響！
      - 如果兩個應用程式都由同一供應商開發，並且使用低於3.7.0的AccessEnabler版本/s，則常規(Adobe)SSO將繼續工作！
      - 如果兩個應用程式都由同一供應商開發並使用AccessEnabler 3.7.0版，則常規(Adobe)SSO將起作用！

1. 如果使用AccessEnabler 3.7.0版將一個應用程式降級到較低版本的AccessEnabler，則不會遷移新生成的令牌。 因此，最終用戶可能會在不期望的情況下體驗到身份驗證/授權會話的丟失。

   - **重要提示：**
      - 通過系統級(Apple)SSO驗證的最終用戶不會受到影響！
      - 在使用AccessEnabler 3.7.0版更新到新應用程式之前已經過身份驗證的最終用戶將不受影響！

1. 如果使用AccessEnabler 3.7.0版將一個應用程式降級到較低版本的AccessEnabler，則不會確認刪除的令牌。 因此，最終用戶可能會體驗到身份驗證/授權會話的存在，而不期望它出現。
