---
title: 如何使用Adobe的API測試網站來測試驗證和授權流程
description: 如何使用Adobe的API測試網站來測試驗證和授權流程
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# 如何使用Adobe的API測試網站來測試驗證和授權流程 {#How-to-test-auth-flows}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

為了測試AuthN和AuthZ流，我們已準備 **API測試網站** 由您自行決定。 我們的支援團隊很樂意為您提供認證。 您可以聯繫我們，地址是 **support@tve.zendesk.com**.


## 第一部分 {#part-I}

要針對RELEASE環境進行測試，請直接跳到第II部分。  若要在資格預審環境中進行測試，請參閱 [在準年前設定您的環境和測試](/help/authentication/setting-up-your-environment-and-testing-in-prequal.md).

## 第二部分

完成第一部分後，執行以下步驟：


1. 開啟網頁： [測試API測試](https://sp.auth-staging.adobe.com/apitest/api.html).
1. 從以下URL載入訪問啟用碼：
   * [用於測試的訪問啟用程式javascript](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js).
   * 或
   * [生產環境的Access啟用程式javascript](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
   * 然後按一下「**Load Access Enabler**」按鈕。
1. 現在將要求者ID值設為「**requestorID**&#x200B;並按一下「setRequestor」按鈕。
1. 之後按下「getAuthentication」按鈕，並等待顯示選擇器顯示。
1. 選取「**MVPD**」。
1. 在「**MVPD**」登入頁面。
1. 重新導向回，重做步驟1到3
1. 在「setAuthenticationStatus」上重新執行步驟3後，應該會看到值「1」。 如果驗證無法運作，則會顯示MVPD對話方塊。
1. 要測試授權，請在資源輸入欄位中輸入「**requestorID**&#x200B;然後按一下「getAuthorization」按鈕。
1. 因此，在&quot;setToken&quot;-\>&quot;resource id&quot;文字方塊中，會顯示資源，而在&quot;setToken&quot;-\>&quot;token&quot;文字方塊中，將會顯示shortAuthorizationToken，表示authZ成功。
1. 現在您可以按一下「登出」按鈕以刪除代號。

