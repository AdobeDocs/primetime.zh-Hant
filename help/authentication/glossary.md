---
title: 字彙表
description: 字彙表
exl-id: e64a94f6-7460-4aa8-8d6b-e0553ba1e4ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# 字彙表 {#glossary}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

## AccessEnabler {#accessEnabler}

Adobe Primetime驗證的使用者端元件。 Adobe Primetime驗證為每個支援的平台提供AccessEnabler程式庫。

## AuthN {#authn}

用作「驗證」的簡稱，如「AuthN代號」或「AuthN流量」。


## AuthN權杖{#authn-token}

驗證權杖，在使用者透過MVPD成功驗證後由Adobe Primetime驗證產生。 根據程式設計師的整合平台，代號會儲存在使用者的裝置上或Adobe Primetime驗證伺服器上。

## AuthZ {#authz}

用作「授權」的簡稱，如「AuthZ代號」或「AuthZ流量」。

## AuthZ權杖 {#authz-token}

授權權杖，在使用者獲得授權可檢視受保護的內容後，由Adobe Primetime驗證產生。 AuthZ權杖儲存在Adobe Primetime驗證伺服器上，並用來產生 [短期媒體Token](#short-lived-token).

## 管道ID （已棄用） {#channel_id}

資源ID的前一個辭彙。

## 無使用者端API {#clientless-api}

採用Web服務（而非AccessEnabler使用者端元件）的Adobe Primetime驗證整合解決方案。

## 裝置ID {#device-id}

可唯一識別裝置（例如手機、平板電腦等） 在Adobe Primetime驗證中。 此ID由程式設計師的應用程式取得/提供。


## 權益流程{#entitlement_flow}

Adobe Primetime驗證檔案中使用的術語，是指使用Adobe Primetime驗證註冊裝置/使用者、使用MVPD驗證使用者、為使用者授權資源以及登出使用者的整個過程。


## GUID {#guid}

另請參閱 [使用者ID](#user-id).

## IdP {#idp}

識別提供者；在Adobe Primetime驗證整合中，MVPD角色的內容與MVPD同義。 （客戶必須透過其付費電視提供者的登入頁面驗證其身分。）

## 媒體權杖驗證器 {#media-token-verifier}

Adobe提供的資料庫，程式設計師可使用此資料庫，驗證Adobe Primetime驗證在成功完成權利流程後產生的短期媒體權杖。

## MVPD {#mvpd}

多頻道視訊節目經銷商；與「付費電視供應商」同義。

## MVPD ID {#mvpd-id}

另請參閱 [使用者ID](#user-id).

## 合作夥伴ID {#partner-id}

Adobe傳遞給MVPD的識別碼，MVPD會用它來識別Adobe Primetime驗證請求驗證的是誰的代表。 有時用於為特定程式設計人員設定其UI，有時用於所有程式設計人員都一樣，這取決於MVPD的需求。

## 付費電視提供者 {#pay-tv-provider}

同義詞 [MVPD](#mvpd).

## 程式設計師 {#programmer}

與「內容提供者」、「帳戶」、「管道」、「服務提供者」、「品牌」等同義。

## Proxy MVPD {#proxy-mvpd}

提供其他MVPD的身分識別服務的MVPD；直接與Adobe Primetime驗證整合。

## 代理的MVPD {#proxied-mvpd}

與AdobeSP沒有直接整合，但透過Proxy MVPD整合的MVPD。

## 請求者ID {#requestor-id}

唯一識別 [程式設計師](#programmer) Adobe Primetime （帳戶、品牌、管道或屬性）。 此ID是在帳戶初始設定期間在程式設計師和Adobe之間決定。 在網路上，請求者ID與已列入白名單的網域相關聯；任何使用來自外部網域的ID的呼叫都將被拒絕。 程式設計師也會將請求者ID用於分析。 每個程式設計師通常只有一個要求者ID。 與請求者ID相關的另一個功能是，程式設計師必須向Adobe提供公開憑證，因為setRequestor API呼叫預期會傳送加密的資料，以用於驗證Adobe Primetime驗證系統中的程式設計師。

## 資源ID {#resource-id}

可識別 [程式設計師](#programmer) 至MVPD。 這由程式設計師和MVPD商定；Adobe Primetime驗證會傳遞資源ID而不被接觸，因此它對於所有MVPD都必須相同。 只要MVPD知道每個ID代表的意義，程式設計師就可以使用多個資源ID。

## SessionGUID {#sessionGUID}

另請參閱 [使用者ID](#user-id).

## 短期媒體Token {#short-lived-token}

此Token是由Adobe Primetime驗證在成功完成特定使用者的權益程式後產生。 權杖會傳遞至程式設計師，程式設計師在短期媒體權杖上使用Adobe Primetime驗證權杖驗證器，驗證授權程式的安全性。

## 智慧型裝置 {#smart-device}

在Adobe Primetime驗證檔案中使用的術語，是指機頂盒、遊戲主機和智慧型電視。 這些裝置具備網路功能，但無法轉譯網頁。

## SP{#sp}

服務提供者；這通常指 *角色* SP的ID (由Adobe Primetime驗證播放)，代表程式設計師與 [MVPD](#mvpd).

## 暫時通過 {#temp-pass}

可讓程式設計師提供臨時免費存取權，以支付內容的功能。 對於程式設計師指定的時段，存取權是每個請求者。

## TTL {#ttl}

存留時間。 這是指定的權杖有效時間長度。

## TVE {#tve}

到處都是電視。

## 使用者ID {#user-id}

唯一識別程式設計師應用程式的使用者，但源自MVPD。 適用於不同使用案例的不同表格。 另請參閱 [瞭解程式設計師概觀中的使用者ID](/help/authentication/programmer-overview.md#user-ids).

## 允許清單 {#whitelist}

為了與Adobe Primetime驗證通訊而指定為合法的網域清單。

## XSTS權杖 {#xsts-token}

由Microsoft所核發的用於Xbox主控台應用程式開發的安全性權杖，用於Xbox/Adobe Primetime驗證整合。
