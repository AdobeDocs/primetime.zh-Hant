---
title: 最低系統需求
description: 最低系統需求
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# 最低系統需求 {#minimum-system-requirements}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。


## 概述 {#overview}

本檔案說明在支援的平台上實作Adobe Primetime驗證整合的目前軟體和硬體需求。 下列所有支援的網頁/行動瀏覽器和作業系統均可受益於Adobe Primetime驗證團隊的完整支援，並符合同意的SLA。

雖然身為Adobe Primetime驗證團隊，我們鼓勵使用最新穩定版本的瀏覽器和作業系統；我們也確認目前使用的不相容/舊版平台和瀏覽器的存在。 這些過時的設備仍可能沒有問題，但更容易出錯。

緩解這些過時平台上出現的任何問題的初始方法應升級至最新版本；這可以是作業系統版本、瀏覽器版本或已安裝應用程式的版本。

Adobe Primetime驗證團隊會盡力解決這些平台上出現的任何問題。 

Adobe Primetime鼓勵我們的客戶和合作夥伴考慮升級至最新版本，以便除提升效能、效率和安全性外，還能從Adobe在任何潛在問題上的完整支援中受益。 


## 瀏覽器和作業系統需求 {#browser-OS-system-requirements}


| 網頁/行動瀏覽器(†) | 支援的版本 |
|---|---|
| Google Chrome | **70** 或更新版本 |
| Mozilla Firefox | **57** 或更新版本 |
| Apple Safari | **14** 或更新版本 |
| Microsoft Edge | **100** 或更新版本 |

(†)Adobe建議不要使用私人或無痕模式。

| 作業系統 | 支援的版本 |
|---|---|
| *Android* | **7.0** (Nougat)或更新版本 |
| *iOS* | **14** 或更新版本 |
| *iPadOS* | **14** 或更新版本 |
| *tvOS* | **14** 或更新版本 |
| *Fire OS* | **5(Android 5.1)** 或更新版本 |
| *Mac OS* | **10.13** 或更新版本 |
| *Microsoft Windows* | **10** 或更新版本 |




>[!NOTE]
>
>第三方Cookie — 停用第三方Cookie時，Adobe Primetime驗證權限流程可能會失敗。  此問題只會在修改瀏覽器設定時傳入播放。 對於所有支援的瀏覽器，Primetime驗證應可搭配預設設定運作。\
 

## 無客戶端(REST)實施的設備要求 {#general_clientless_reqs}

 
透過無用戶端實作使用Adobe Primetime驗證服務的任何裝置 **必須能**:

* 提供不重複的雜湊裝置ID。 如果裝置未提供唯一雜湊裝置ID，則必須能保留Adobe Primetime驗證提供的唯一ID。 裝置應能將唯一ID永久保留在本機儲存空間，並在呼叫Adobe Primetime Authentication API時提供唯一ID作為裝置ID。
* 使用HMAC-SHA1演算法產生數位簽名
* 設定任意HTTP標頭
* 使用RESTful Web服務
* 剖析XML和JSON資料格式
* 使用HTTPS傳送流量
* 處理HTTP錯誤代碼
