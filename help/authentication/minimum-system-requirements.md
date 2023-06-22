---
title: 最低系統需求
description: 最低系統需求
exl-id: 57b21e2a-abd7-4b4b-85f1-25584a850e40
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 最低系統需求 {#minimum-system-requirements}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。


## 概觀 {#overview}

本檔案說明在支援平台上實施Adobe Primetime驗證整合的目前軟體和硬體需求。 以下列出的所有支援網頁/行動瀏覽器和作業系統都將受益於Adobe Primetime驗證團隊的完整支援，其須遵守同意的SLA。

身為Adobe Primetime驗證團隊，我們鼓勵使用最新穩定版本的瀏覽器和作業系統；我們也承認存在目前使用的不相容/舊版平台和瀏覽器。 這些過時裝置仍可正常運作，但更容易出錯。

緩解這些過時平台上出現之任何問題的初始方法，應該是升級至最新版本；這可以是作業系統版本、瀏覽器版本或已安裝應用程式的版本。

Adobe Primetime驗證團隊會盡最大努力解決這些平台上出現的任何問題。 

Adobe Primetime鼓勵我們的客戶和合作夥伴考慮升級至最新版本，除了提升效能、效率和安全性外，還可在任何潛在問題中受益於Adobe的完整支援。 


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
| *引發作業系統* | **5 (Android 5.1)** 或更新版本 |
| *Mac作業系統* | **10.13** 或更新版本 |
| *Microsoft Windows* | **10** 或更新版本 |




>[!NOTE]
>
>第三方Cookie — 停用第三方Cookie時，Adobe Primetime驗證權益流程可能會失敗。  此問題只會在瀏覽器設定被修改時才會出現。 對於所有支援的瀏覽器，Primetime驗證應該可以使用預設設定來運作。\
 

## 無使用者端(REST)實作的裝置需求 {#general_clientless_reqs}

 
任何會透過無使用者端實作使用Adobe Primetime驗證服務的裝置 **必須能夠**：

* 提供唯一的雜湊裝置ID。 如果裝置未提供唯一的雜湊裝置ID，則必須能儲存由Adobe Primetime驗證提供的唯一ID。 裝置應該能夠永久儲存唯一ID至其本機儲存空間，並在呼叫Adobe Primetime驗證API時提供唯一ID作為裝置ID。
* 使用HMAC-SHA1演演算法產生數位簽名
* 設定任意HTTP標頭
* 使用RESTful Web服務
* 剖析XML和JSON資料格式
* 使用HTTPS傳送流量
* 處理HTTP錯誤代碼
