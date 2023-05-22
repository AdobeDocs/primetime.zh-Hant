---
title: 辭彙表
description: 辭彙表
exl-id: e64a94f6-7460-4aa8-8d6b-e0553ba1e4ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# 辭彙表 {#glossary}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

## AccessEnabler {#accessEnabler}

Adobe Primetime身份驗證的客戶端元件。 Adobe Primetime驗證為每個支援的平台提供了AccessEnabler庫。

## 身份驗證 {#authn}

用作「身份驗證」的簡寫，如「AuthN令牌」或「AuthN流」中。


## AuthN令牌{#authn-token}

驗證令牌，由Adobe Primetime驗證在用戶成功使用MVPD驗證後生成。 根據程式設計師的整合平台，令牌儲存在用戶設備或Adobe Primetime驗證伺服器上。

## 身份驗證 {#authz}

用作「授權」的簡寫，如「AuthZ令牌」或「AuthZ流」中。

## AuthZ令牌 {#authz-token}

授權令牌，由Adobe Primetime身份驗證在用戶被授權查看受保護內容後生成。 AuthZ令牌儲存在Adobe Primetime驗證伺服器上，用於生成 [短期媒體令牌](#short-lived-token)。

## 通道ID（不建議使用） {#channel_id}

資源ID的前一個術語。

## 無客戶端API {#clientless-api}

一種Adobe Primetime身份驗證整合解決方案，它使用Web服務而不是AccessEnabler客戶端元件。

## 設備ID {#device-id}

唯一標識設備（如電話、平板電腦等） 在Adobe Primetime驗證中。 此ID由程式設計師的應用程式獲取/提供。


## 權利流{#entitlement_flow}

Adobe Primetime驗證文檔中使用的術語是指將設備/用戶註冊到Adobe Primetime驗證、使用MVPD驗證用戶、為用戶授權資源以及註銷用戶的整個過程。


## GUID {#guid}

請參閱 [用戶ID](#user-id)。

## IDP {#idp}

識別提供方；與MVPD在Adobe Primetime身份驗證整合中的角色的上下文中的MVPD同義。 （客戶必須通過付費電視提供商的登錄頁驗證其身份。）

## 媒體令牌驗證器 {#media-token-verifier}

Adobe提供的庫，由程式設計師在權利流成功完成後，用於驗證由Adobe Primetime身份驗證生成的短時媒體令牌。

## MVPD {#mvpd}

多通道視頻節目分發商；同義於「付費電視提供商」。

## MVPD ID {#mvpd-id}

請參閱 [用戶ID](#user-id)。

## 合作夥伴ID {#partner-id}

Adobe傳遞給MVPD的標識符，MVPD使用它來標識其代表的Adobe Primetime身份驗證正在請求身份驗證。 它有時用於為特定程式設計師配置其UI，有時在所有程式設計師中都是相同的，它取決於MVPD的需要。

## 付費電視提供商 {#pay-tv-provider}

同義詞 [MVPD](#mvpd)。

## 程式設計師 {#programmer}

等同於「內容提供商」、「帳戶」、「渠道」、「服務提供商」、「品牌」等。

## 代理MVPD {#proxy-mvpd}

為其他MVPD提供標識服務的MVPD;直接與Adobe Primetime驗證整合。

## 代理MVPD {#proxied-mvpd}

未與AdobeSP直接整合，但通過代理MVPD整合的MVPD。

## 請求者ID {#requestor-id}

唯一標識 [程式設計師](#programmer) （帳戶、品牌、渠道或財產）在Adobe Primetime驗證中。 此ID在帳戶的初始設定期間由程式設計師和Adobe確定。 在Web上，請求者ID與一組白名單域相關聯；使用外部域ID的任何呼叫都將被拒絕。 程式設計師還使用請求程式ID進行分析。 每個程式設計師通常只有一個請求者ID。 與請求者ID相關的另外一個特徵是程式設計師必須向Adobe提供公共證書，因為setRequestor API調用期望發送加密資料，用於在Adobe Primetime認證系統中對程式設計師進行認證。

## 資源ID {#resource-id}

標識一個 [程式設計師](#programmer) 到MVPD。 程式設計師和MVPD之間商定；Adobe Primetime身份驗證將資源ID通過未觸發，因此對於所有MVPD必須相同。 只要MVPD知道每個ID代表什麼，程式設計師就可以使用多個資源ID。

## 會話GUID {#sessionGUID}

請參閱 [用戶ID](#user-id)。

## 短期媒體令牌 {#short-lived-token}

此令牌是在特定用戶的授權過程成功完成後由Adobe Primetime驗證生成的。 令牌將傳遞給程式設計師，程式設計師在短時間媒體令牌上使用Adobe Primetime驗證令牌驗證器來驗證權利進程的安全性。

## 智慧設備 {#smart-device}

在整個Adobe Primetime驗證文檔中使用的術語指機頂盒、遊戲機和智慧電視。 這些設備具有網路功能，但無法呈現網頁。

## SP{#sp}

服務提供商；這通常是指 *角色* SP，由Adobe Primetime驗證播放，在與 [MVPD](#mvpd)。

## 臨時通過 {#temp-pass}

一種功能，使程式設計師能夠臨時免費訪問付費內容。 在程式設計師指定的時間段內，訪問是每個請求者。

## TTL {#ttl}

該活了。 這是令牌有效的指定時間長度。

## 鄉鎮 {#tve}

電視無處不在。

## 用戶ID {#user-id}

唯一標識程式設計師應用的用戶，但從MVPD組織。 可在不同的表單中提供，用於不同的使用案例。 請參閱 [瞭解程式設計師概述中的用戶ID](/help/authentication/programmer-overview.md#user-ids)。

## 允許清單 {#whitelist}

為與Adobe Primetime身份驗證通信而指定為合法的域的清單。

## XSTS令牌 {#xsts-token}

Microsoft為Xbox主機應用開發頒發的安全令牌，用於Xbox/Adobe Primetime身份驗證整合。
