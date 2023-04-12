---
title: REST API逐步指南（用戶端對伺服器）
description: 將API逐步指南用戶端置於伺服器。
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---


# REST API逐步指南（用戶端對伺服器） {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 概述 {#overview}

本文檔為程式設計師的工程團隊提供逐步指示，以整合「智慧設備」（遊戲機、智慧電視應用、機頂盒等） 搭配Adobe Primetime驗證（使用REST API服務）。 此用戶端對伺服器方法使用REST API而非用戶端SDK，可讓不同平台提供更廣泛的支援，而開發大量不重複SDK則無法進行。 如需無客戶解決方案運作方式的廣泛技術概述，請參閱 [無客戶端技術概述](/help/authentication/rest-api-overview.md).


此方法需要兩個元件（串流應用程式和AuthN應用程式）才能完成所需的流程：串流應用程式中的啟動、註冊、授權和檢視媒體流程，以及AuthN應用程式中的驗證流程。

## 元件 {#components}

在有效的客戶端對伺服器解決方案中，涉及以下元件：

 

| 類型 | 元件 | 說明 |
| --- | --- | --- |
| 串流裝置 | 串流應用程式 | 駐留在用戶流設備上並播放已驗證視頻的程式設計師應用程式。 |
|  | \[可選\] AuthN模組 | 如果串流裝置有使用者代理（即Web瀏覽器），則AuthN模組負責在MVPD IdP上驗證使用者。 |
| \[可選\] AuthN設備 | AuthN應用程式 | 如果流設備沒有用戶代理（即Web瀏覽器），則AuthN應用程式是程式設計師Web應用程式，使用Web瀏覽器從單獨的用戶設備訪問。  |
| Adobe基礎結構 | Adobe Pass服務 | 與MVPD IdP和AuthZ服務整合，並提供驗證和授權決策的服務。 |
| MVPD基礎結構 | MVPD IdP | 提供憑證式驗證服務以驗證其使用者身分的MVPD端點。 |
|  | MVPD AuthZ服務 | MVPD端點，可根據使用者的訂閱、家長控制等提供授權決策。 |

 

流量中使用的其他術語定義於 [字彙表](/help/authentication/glossary.md).

## 流量{#flows}

### 動態用戶端註冊(DCR)

Adobe Pass使用DCR來保護程式設計師應用程式或伺服器與Adobe Pass服務之間的客戶端通信。 DCR流程是獨立、相依和先決條件流程，可在 [動態客戶端註冊](/help/authentication/dynamic-client-registration.md)


### 串流（智慧裝置）應用程式流程

![](assets/smart-device-app-flow.png)

#### 啟動流程

1. 您的應用程式會啟動並載入其初始UI。

2. 取得/產生裝置ID。

3. 發出檢查驗證呼叫，查看裝置是否已通過驗證。  例如： [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. 若 `checkauthn` 呼叫成功，從步驟2開始繼續進行授權流程。  如果失敗，請啟動註冊流。

 

#### 註冊流程

1. 取得註冊碼和URL，供您的使用者用來存取您的第2個畫面登入應用程式，並向使用者呈現下列項目：

   a.傳送POST要求至Adobe註冊代碼服務，並傳遞雜湊裝置ID和「註冊URL」。  例如： [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b.將傳回的註冊代碼和URL呈現給使用者。

   c.指示使用者切換至可使用Web的裝置，導覽至URL，然後輸入註冊代碼。

 

#### 授權流程

1. 使用者從第2個畫面應用程式返回，然後按下裝置上的「繼續」按鈕。 或者，您也可以實作輪詢機制以檢查驗證狀態，但Adobe Primetime驗證建議在輪詢上使用Continue按鈕方法。 <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> 例如： [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. 向Adobe Primetime驗證授權服務發送GET請求以啟動授權。 例如： `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

* 如果回應指出成功：使用者具有有效的AuthN權杖，且使用者已獲授權可觀看請求的媒體（此使用者有有效的AuthZ權杖）。

* 如果回應指出失敗：檢查擲回的例外狀況，以判斷其類型（AuthN、AuthZ或其他類型）:

   * 如果是AuthN錯誤，則重新啟動註冊流。

   * 如果是AuthZ錯誤，則用戶無權觀看請求的媒體，應向用戶顯示某種錯誤消息。

   * 如果有其他錯誤（連線錯誤、網路錯誤等） 然後向用戶顯示相應的錯誤消息。

 

#### 檢視媒體流量

1. 提供媒體選擇。 使用者會選取要檢視的媒體。

2. 介質是否受到保護？

   a.您的應用程式會檢查媒體是否受到保護。

   b.如果媒體受到保護，您的應用程式就會啟動上方的授權(AuthZ)流程。

   c.如果介質未受保護，則為用戶播放介質。

3. 播放媒體。


### AuthN（第2螢幕）應用程式流

![](assets/secnd-screen-authn-flow.png)

1. 取得此使用者的MVPD清單。 例如： [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. 啟動驗證流程。  例如： [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. 檢查驗證是否成功。 例如：[`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. 將使用者傳回至您的智慧裝置應用程式以完成授權流程。

## 平台SSO {#platform-sso}

有些平台提供單一登入(SSO)的專屬支援。 可找到每個平台的實作詳細資料：

* [AppleSSO](/help/authentication/apple-sso-cookbook-rest-api.md)
* AmazonSSO

## TempPass和Promotion TempPass for REST API {#temppass}

若是使用者不需要輸入憑證的TempPass和促銷TempPass實作，可直接在串流應用程式中實作驗證。

**若要使用此API，串流應用程式必須確定裝置ID的唯一性，因為此ID用於識別代號，以及選用的額外資料。**


![](assets/temp-pass-promo-temppass.png)

