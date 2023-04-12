---
title: 使用OAuth 2.0通訊協定進行驗證
description: 使用OAuth 2.0通訊協定進行驗證
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# 使用OAuth 2.0通訊協定進行驗證

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## 概述 {#overview}

雖然SAML仍是MVPD和企業普遍使用的主要認證協定，但OAuth 2.0作為主認證協定的趨勢是明顯的。 OAuth 2.0通訊協定(https://tools.ietf.org/html/rfc6749)主要為消費者網站所開發，並迅速被Facebook、Google和Twitter等網際網路巨頭所採用。

OAuth 2.0非常成功，這促使企業緩慢地升級其基礎設施以支援它。



## 移至OAuth 2.0的優點 {#adv-oauth2}

在高層面上，OAuth 2.0通訊協定提供與SAML通訊協定相同的功能，但有一些重要的差異。

其中一個事實是，重新整理Token流可用作在幕後重新整理驗證的方式。 這可讓IdP（此例中為MVPD）維持控制，同時仍可提供良好的使用者體驗，因為出於安全考量，使用者不再需要經常登入。

此通訊協定也提供更大彈性，因為服務提供者現在可以使用代號來存取其他API以取得額外資訊。 這反過來又導致了TVE使用案例的「動產層」協定，但它允許複雜工作流所需的靈活性。





## 切換至OAuth 2.0的需求 {#oauth-req}

若要支援使用OAuth 2.0進行驗證，MVPD必須符合下列必要條件：

首先，MVPD必須確保支援*[授權代碼授予](https://oauthlib.readthedocs.io/en/latest/oauth2/grants/authcode.html) 流量。

確認支援流程後，MVPD必須提供下列資訊：

* 驗證端點
   * 終端點將提供授權碼，此授權碼稍後將用於交換重新整理和存取權杖
* /token端點
   * 這將提供重新整理權杖和存取權杖
   * 重新整理權杖必須穩定(不得在每次請求新存取權杖時變更
   * MVPD需要允許每個重新整理權杖有數個作用中的存取權杖
   * 此端點也會交換存取權杖的重新整理權杖
* 我們需要 **用戶配置檔案的端點**
   * 此端點將提供userID，此ID對於帳戶而言必須是唯一的，且不應包含任何個人識別資訊
* the **/logout** 端點（可選）
   * Adobe Primetime驗證會重新導向至此端點，為MVPD提供重新導向的背面URI;在此端點上，MVPD可清除用戶端電腦上的cookie，或套用任何需要的邏輯以登出
* 強烈建議支援授權客戶端（不觸發用戶授權頁面的客戶端應用）
* 我們還需要：
   * **clientID** 和 **用戶密碼** 整合設定
   * **生命** 重新整理Token和存取Token的(TTL)值
   * 我們可以為MVPD提供授權回呼和註銷回呼URI。 此外，如有需要，我們可以為MVPD提供要列入防火牆設定白名單的IP清單。


## 驗證流程 {#authn-flow}

在驗證流程中，Adobe Primetime驗證會與設定中選取之通訊協定上的MVPD通訊。 OAuth 2.0流量如下圖所示：



![顯示Adobe驗證中的驗證流程的圖表，該流程與配置中所選協定上的MVPD通信。](assets/authn-flow.png)

**圖1:OAuth 2.0驗證流量**



## 驗證要求和回應 {#authn-req-response}

簡而言之，支援OAuth 2.0通訊協定之MVPD的驗證流程會遵循下列步驟：

1. 最終用戶導航到程式設計師的站點，並選擇使用其MVPD憑據登錄
1. 安裝在程式設計師端的AccessEnabler，以HTTP請求的形式向Adobe Primetime身份驗證端點發送身份驗證請求，Adobe Primetime身份驗證端點將重定向到MVPD授權端點。
1. MVPD授權端點會將授權代碼傳送至Adobe Primetime驗證端點
1. Adobe Primetime驗證會使用收到的授權碼，從MVPD的Token端點請求重新整理Token和存取Token
1. 擷取使用者資訊和中繼資料的呼叫可傳送至使用者設定檔端點，以備使用者資訊未包含在Token中時使用
1. 驗證令牌將傳遞給最終用戶，最終用戶現在可以成功瀏覽程式設計師站點

   >[!NOTE]
   >
   >在目前的存取權杖無效或過期後，會使用重新整理權杖來取得新的存取權杖。


>[!IMPORTANT]
>
>重新整理Token在交換為存取Token時不得變更。

此限制來自用戶端流程，這些流程不允許伺服器更新AuthNToken，而對於OAuth 2.0通訊協定，AuthNToken也包含重新整理權杖。

典型授權流程執行保存在AuthNToken中的刷新令牌的交換，該刷新令牌隨後用於以首先被驗證的用戶的名稱執行授權呼叫。 如果授權伺服器(MVPD)要變更重新整理權杖，並使舊的權杖失效，我們將無法更新有效的AuthNToken。 因此，MVPD需要支援穩定的重新整理Token，才能為其設定OAuth 2.0整合。


## 從SAML移轉至OAuth 2.0 {#saml-auth2-migr}

將整合從SAML移轉至OAuth 2.0將由Adobe和MVPD執行。 程式設計師無需進行任何技術更改，儘管程式設計師可能希望在MVPD登錄頁上檢查/測試品牌結合。 從MVPD的觀點來看，需要Oauth 2.0要求中要求的端點和其他資訊。

為了 **保留SSO**，已透過SAML取得驗證Token的使用者仍會被視為已驗證，而其要求將會透過舊版SAML整合路由。

從技術角度來看：

1. Adobe可讓程式設計人員與MVPD之間進行OAuth 2.0整合，而不會刪除SAML整合。
1. 啟用後，所有新使用者都會使用OAuth 2.0流程。
1. 已驗證且已具有包含SAML主體ID之本機AuthN代號的使用者，將會透過SAML整合由Adobe自動路由。
1. 對於步驟3中的使用者，一旦其SAML產生的AuthN代號過期，Adobe就會將他們視為新使用者，並像步驟2中的使用者一樣處理。
1. Adobe將檢閱使用模式，以決定SAML整合可安全停用的時機。

