---
title: 使用OAuth 2.0協定進行身份驗證
description: 使用OAuth 2.0協定進行身份驗證
exl-id: 0c1f04fe-51dc-4b4d-88e7-66e8f4609e02
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# 使用OAuth 2.0協定進行身份驗證

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## 概述 {#overview}

雖然SAML協定仍是美國MVPD和企業普遍使用的主要認證協定，但OAuth 2.0作為主認證協定的趨勢是明顯的。 OAuth 2.0協定(https://tools.ietf.org/html/rfc6749)主要為消費者網站開發，並很快被Facebook、Google和Twitter等網際網路巨頭採納。

OAuth 2.0非常成功，這促使企業緩慢地升級其基礎架構以支援它。



## 遷移到OAuth 2.0的優勢 {#adv-oauth2}

在高級別上，OAuth 2.0協定提供的功能與SAML協定相同，但有一些重要的區別。

其中一個事實是，刷新令牌流可用作在幕後刷新身份驗證的一種方式。 這允許IdP（本例中的MVPD）維護控制，同時仍允許良好的用戶體驗，因為出於安全考慮，用戶不再需要經常登錄。

該協定還提供了更大的靈活性，因為服務提供商現在可以使用令牌訪問其他API來獲取額外資訊。 這反過來又為TVE使用案例提供了一個「動產層」協定，但它允許複雜工作流所需的靈活性。





## 切換到OAuth 2.0的要求 {#oauth-req}

要支援使用OAuth 2.0進行身份驗證，MVPD需要滿足以下先決條件：

首先，MVPD必須確保它支援*[授權代碼授予](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) 。

在確認它支援流後，MVPD必須提供以下資訊：

* 驗證端點
   * 終端點將提供授權碼，稍後將用以交換刷新和訪問令牌
* /token端點
   * 這將提供刷新令牌和訪問令牌
   * 刷新令牌需要穩定(它不得在每次請求新訪問令牌時更改
   * MVPD需要為每個刷新令牌允許多個活動訪問令牌
   * 此終端點還將為訪問令牌交換刷新令牌
* 我們需要 **用戶配置檔案的端點**
   * 此終點將提供userID，該用戶ID對於帳戶來說必須唯一，並且不應包含任何個人身份資訊
* 這樣 **/logout** 端點（可選）
   * Adobe Primetime認證將重定向到此終點，為MVPD提供重定向回URI;在此終點上，MVPD可以清除客戶端電腦上的cookie或應用註銷所需的任何邏輯
* 強烈建議支援授權客戶端（不觸發用戶授權頁的客戶端應用）
* 我們還需要：
   * **客戶端ID** 和 **客戶端機密** 用於整合配置
   * **活到** 刷新令牌和訪問令牌的(TTL)值
   * 我們可以為MVPD提供授權回調和註銷回調URI。 此外，如果需要，我們可以向MVPD提供要在防火牆設定中白列出的IP清單。


## 驗證流 {#authn-flow}

在驗證流中，Adobe Primetime驗證將與配置中選擇的協定上的MVPD通信。 OAuth 2.0流如下圖所示：



![用於顯示與配置中選定協定上的MVPD通信的Adobe驗證中的驗證流的圖。](assets/authn-flow.png)

**圖1:OAuth 2.0驗證流**



## 身份驗證請求和響應 {#authn-req-response}

簡而言之，支援OAuth 2.0協定的MVPD的驗證流遵循以下步驟：

1. 最終用戶導航到程式設計師站點，並選擇使用其MVPD憑據登錄
1. 安裝在程式設計師側的AccessEnabler向Adobe Primetime驗證終結點發送HTTP請求形式的驗證請求，Adobe Primetime驗證終結點將該HTTPD驗證終結點重定向到MVPD授權終結點。
1. MVPD授權端點向Adobe Primetime身份驗證端點發送授權代碼
1. Adobe Primetime驗證使用接收的授權代碼從MVPD的令牌端點請求刷新令牌和訪問令牌
1. 當用戶資訊未包括在令牌中時，可以將獲取用戶資訊和元資料的呼叫發送到用戶配置檔案端點
1. 驗證令牌將傳遞給現在可以成功瀏覽程式設計師站點的最終用戶

   >[!NOTE]
   >
   >刷新令牌用於在當前訪問令牌無效或過期後獲取新訪問令牌。


>[!IMPORTANT]
>
>在將刷新令牌交換為訪問令牌時，不能更改它。

此限制源於客戶端流，這些流不允許伺服器更新AuthNToken，對於OAuth 2.0協定，AuthNToken還包含刷新令牌。

典型授權流執行在AuthNToken中保存的用於訪問令牌的刷新令牌的交換，該訪問令牌隨後被用於以在最初被認證的用戶的名稱執行授權調用。 如果授權伺服器(MVPD)要更改刷新令牌並使舊令牌失效，我們將無法更新有效的AuthNToken。 因此，MVPD需要支援穩定的刷新令牌才能為其設定OAuth 2.0整合。


## 從SAML遷移到OAuth 2.0 {#saml-auth2-migr}

將整合從SAML遷移到OAuth 2.0將通過Adobe和MVPD執行。 在程式設計師方面不需要進行任何技術更改，儘管程式設計師可能希望在MVPD登錄頁上檢查/test聯合品牌。 從MVPD的角度，需要Oauth 2.0要求中請求的端點和其他資訊。

為了 **保留SSO**，通過SAML獲取的已具有身份驗證令牌的用戶仍將被視為經過身份驗證，其請求將通過舊的SAML整合進行路由。

從技術角度來看：

1. Adobe將允許程式設計師和MVPD之間進行OAuth 2.0整合，而不刪除SAML整合。
1. 啟用後，所有新用戶都將使用OAuth 2.0流。
1. 已經過身份驗證的用戶（已具有包含SAML subject-id的本地AuthN令牌）將通過SAML整合Adobe自動路由。
1. 對於步驟3中的用戶，一旦其SAML生成的AuthN令牌過期，Adobe將視其為新用戶，並像步驟2中的用戶一樣行為。
1. Adobe將審查使用模式，以確定SAML整合可以安全停用的時間。
