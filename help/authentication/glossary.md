---
title: 字彙表
description: 字彙表
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# 字彙表 {#glossary}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

## AccessEnabler {#accessEnabler}

Adobe Primetime驗證的用戶端元件。 Adobe Primetime身份驗證為每個受支援的平台提供一個AccessEnabler庫。

## AuthN {#authn}

作為「authentication」的簡稱，如「AuthN Token」或「AuthN流量」。


## AuthN代號{#authn-token}

驗證Token，在使用者透過MVPD成功驗證後，由Adobe Primetime驗證產生。 根據程式設計師的整合平台，令牌儲存在用戶設備或Adobe Primetime驗證伺服器上。

## AuthZ {#authz}

作為「授權」的簡稱，例如「AuthZ代號」或「AuthZ流量」。

## AuthZ代號 {#authz-token}

授權Token，在使用者獲得檢視受保護內容的授權後，由Adobe Primetime驗證產生。 AuthZ代號儲存在Adobe Primetime驗證伺服器上，並用來產生 [短期媒體代號](#short-lived-token).

## 管道ID（已淘汰） {#channel_id}

資源ID的前一個詞。

## 無用戶端API {#clientless-api}

採用Web服務而非AccessEnabler客戶端元件的Adobe Primetime身份驗證整合解決方案。

## 裝置ID {#device-id}

唯一識別裝置（例如手機、平板電腦等） 在Adobe Primetime驗證中。 該ID由程式設計師的應用程式獲得/提供。


## 權利流程{#entitlement_flow}

Adobe Primetime驗證檔案中使用的辭彙，是指透過Adobe Primetime驗證註冊裝置/使用者、使用MVPD驗證使用者、為使用者授權資源，以及登出使用者的整個程式。


## GUID {#guid}

請參閱 [使用者ID](#user-id).

## IdP {#idp}

識別提供者；等同於MVPD在Adobe Primetime驗證整合中角色的內容。 （客戶必須透過付費電視提供者的登入頁面驗證其身分）。

## 媒體令牌驗證器 {#media-token-verifier}

程式設計人員用來驗證Adobe Primetime驗證在權限流程成功完成後產生的短期媒體權杖的Adobe提供的程式庫。

## MVPD {#mvpd}

多通道視頻節目分發商；與「付費電視提供者」同義。

## MVPD ID {#mvpd-id}

請參閱 [使用者ID](#user-id).

## 合作夥伴ID {#partner-id}

Adobe傳遞給MVPD的識別碼，MVPD可讓MVPD用來識別代表Adobe Primetime驗證要求驗證的身分。 有時，它是用於為特定程式設計師配置其UI，有時它在所有程式設計師中都一樣，它取決於MVPD的需求。

## 付費電視提供者 {#pay-tv-provider}

同義於 [MVPD](#mvpd).

## 程式設計師 {#programmer}

同義於「內容提供者」、「帳戶」、「頻道」、「服務提供者」、「品牌」等。

## 代理MVPD {#proxy-mvpd}

為其他MVPD提供身分服務的MVPD;直接與Adobe Primetime驗證整合。

## 代理的MVPD {#proxied-mvpd}

未與AdobeSP直接整合，但透過Proxy MVPD整合的MVPD。

## 請求者ID {#requestor-id}

唯一識別 [程式設計師](#programmer) （帳戶、品牌、管道或屬性）。 此ID在初始設定帳戶期間由程式設計師和Adobe確定。 在網路上，請求者ID與一組白名單網域相關聯；任何使用來自外部網域之ID的呼叫將遭拒。 程式設計師也會使用Analytics的要求者ID。 每個程式設計師通常只有一個請求者ID。 與請求者ID相關的另一項功能是程式設計師必須向Adobe提供公共證書，因為setRequestor API調用期望發送加密資料，用於驗證Adobe Primetime驗證系統中的程式設計師。

## 資源ID {#resource-id}

用於識別 [程式設計師](#programmer) 到MVPD。 程式設計師與MVPD之間商定；Adobe Primetime驗證會將資源ID傳至未變更的ID，因此所有MVPD都必須相同。 只要MVPD知道每個ID代表什麼，程式設計師就可以使用多個資源ID。

## SessionGUID {#sessionGUID}

請參閱 [使用者ID](#user-id).

## 短期媒體代號 {#short-lived-token}

此代號是在特定使用者的授權程式成功完成時，由Adobe Primetime驗證產生。 令牌會傳遞給程式設計師，他們使用短期媒體令牌上的Adobe Primetime驗證令牌驗證器來驗證權限過程的安全性。

## 智慧裝置 {#smart-device}

在整個Adobe Primetime驗證檔案中使用的辭彙，是指機上盒、遊戲主機和智慧電視。 這些設備具有網路功能，但無法呈現網頁。

## SP{#sp}

服務提供商；這通常指 *角色* 由Adobe Primetime驗證播放，代表程式設計師與 [MVPD](#mvpd).

## 臨時通道 {#temp-pass}

一種功能，可讓程式設計人員提供支付內容的臨時免費存取。 在程式設計師指定的時間段內，按請求者訪問。

## TTL {#ttl}

活下來了。 這是Token有效的指定時間長度。

## TVE {#tve}

電視無處不在。

## 使用者ID {#user-id}

唯一識別程式設計師應用程式的使用者，但從MVPD組織。 可針對不同使用案例以不同形式提供。 請參閱 [了解程式設計師概覽中的用戶ID](/help/authentication/programmer-overview.md#user-ids).

## 允許的清單 {#whitelist}

為了與Adobe Primetime驗證通訊而指定為合法的網域清單。

## XSTS代號 {#xsts-token}

由Microsoft發出的用於Xbox/Adobe Primetime驗證整合的安全令牌，用於Xbox/Xbox控制台應用程式開發。
