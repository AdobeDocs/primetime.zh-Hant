---
title: 如何使用Adobe的APItest站點test驗證和授權流
description: 如何使用Adobe的APItest站點test驗證和授權流
exl-id: 04af4aed-35e4-44cb-98ce-7643165a8869
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 如何使用Adobe的APItest站點Test驗證和授權流 {#How-to-test-auth-flows}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

為了testAuthN和AuthZ流，我們準備了 **APItest站點** 你可以隨便。 我們的支援團隊將樂意為您提供憑據。 你可以聯繫我們 **support@tve.zendesk.com**。


## 第一部分 {#part-I}

要針對RELEASE環境進行測試，請直接跳至第II部分。  要在資格預審環境中test，請參見 [在準年前設定環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md)。

## 第二部分

完成第I部分後，執行以下步驟：


1. 開啟網頁： [暫存APItest](https://sp.auth-staging.adobe.com/apitest/api.html)。
1. 從以下URL載入訪問啟用碼：
   * [用於暫存的Access啟用程式Javascript](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js)。
   * 或
   * [用於生產的Access啟用程式Javascript](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js)。
   * 然後按一下「 」**載入Access啟用碼**&#x200B;按鈕
1. 現在將請求者ID值設定為「」**請求者ID**&quot; ，然後按一下&quot;setRequestor&quot;按鈕。
1. 然後按「getAuthentication」按鈕，等待顯示選取器顯示。
1. 選擇「」**MVPD**&#x200B;的子菜單。
1. 在「 」上輸入您的憑據&#x200B;**MVPD**」登錄頁。
1. 重定向回後，重做步驟1至3
1. 在「setAuthenticationStatus」上重新執行步驟3後，應看到值「1」。 如果驗證無效，則將顯示MVPD對話框。
1. 要test授權，請在資源輸入欄位中輸入「**請求者ID**&quot; ，然後按一下&quot;getAuthorization&quot;按鈕。
1. 因此，在&quot;setToken&quot;-\>&quot;resource id&quot;文本框中將顯示資源，在&quot;setToken&quot;-\>&quot;token&quot;文本框中將顯示shortAuthorizationToken，表示authZ成功。
1. 現在，您可以按一下「註銷」按鈕以刪除令牌。
