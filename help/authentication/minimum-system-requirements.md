---
title: 最低系統要求
description: 最低系統要求
exl-id: 57b21e2a-abd7-4b4b-85f1-25584a850e40
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 最低系統要求 {#minimum-system-requirements}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。


## 概述 {#overview}

本文檔介紹了在受支援平台上實施Adobe Primetime身份驗證整合的當前軟體和硬體要求。 下面列出的所有支援的Web/移動瀏覽器和作業系統都將受益於Adobe Primetime身份驗證團隊的全面支援，這些支援與商定的SLA相符。

作為Adobe Primetime認證團隊，我們鼓勵使用瀏覽器和作業系統的最新版本；我們還確認存在當前正在使用的不相容/舊平台和瀏覽器。 這些過時的設備仍可能運行時沒有問題，但它們更容易出錯。

緩解這些過時平台上出現的任何問題的初始方法應升級到最新版本；這可以是作業系統版本、瀏覽器版本或已安裝應用程式的版本。

這些平台上出現的任何問題都將由Adobe Primetime身份驗證團隊以盡力解決。 

Adobe Primetime鼓勵我們的客戶和合作夥伴考慮升級到最新版本，以便除效能、效率和安全性改進外，在任何潛在問題上都能獲得Adobe的全面支援。 


## 瀏覽器和作業系統要求 {#browser-OS-system-requirements}


| Web/Mobile瀏覽器(†) | 支援的版本 |
|---|---|
| Google鉻 | **70** 或 |
| Mozilla Firefox | **57** 或 |
| Apple野生動物園 | **14** 或 |
| Microsoft邊 | **100** 或 |

(†)Adobe建議不要使用私人或隱姓埋名模式。

| 作業系統 | 支援的版本 |
|---|---|
| *安卓* | **7.0** （努加特）或更高版本 |
| *iOS* | **14** 或 |
| *iPadOS* | **14** 或 |
| *電視作業系統* | **14** 或 |
| *Fire OS* | **5(Android 5.1)** 或 |
| *MacOS* | **10.13** 或 |
| *Microsoft窗* | **10** 或 |




>[!NOTE]
>
>第3方Cookie — 禁用第3方Cookie時，Adobe Primetime身份驗證權利流可能會失敗。  僅當修改瀏覽器設定時才會播放此問題。 對於所有支援的瀏覽器，黃金時段身份驗證應使用預設設定。\
 

## 無客戶端(REST)實現的設備要求 {#general_clientless_reqs}

 
通過無客戶端實施使用Adobe Primetime身份驗證服務的任何設備 **必須能夠**:

* 提供唯一的散列設備ID。 如果設備未提供唯一散列的設備ID，則它必須能夠保留由Adobe Primetime身份驗證提供的唯一ID。 設備應能夠永久保留其本地儲存中的唯一ID，並在調用Adobe Primetime驗證API時提供唯一ID作為設備ID。
* 使用HMAC-SHA1算法生成數字簽名
* 設定任意HTTP標頭
* 使用REST風格的Web服務
* 分析XML和JSON資料格式
* 使用HTTPS發送通信
* 處理HTTP錯誤代碼
