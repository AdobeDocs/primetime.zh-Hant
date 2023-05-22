---
title: Adobe Primetime身份驗證2.64發行說明
description: Adobe Primetime身份驗證2.64發行說明
exl-id: 4db21026-a0c2-4e33-b01f-4ccae824a110
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Adobe Primetime身份驗證2.64發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

本頁介紹此版本的新功能、更改和已知問題：

## 伺服器端和Web客戶端 {#ss-web-clients}

* [內部版本號](#build-no-264)
* [新功能](#new-featres-264)
* [錯誤修復](#bug-fixes-264)


### 內部版本號 {#build-no-264}

Adobe Primetime驗證：adobe-pass-**二塊六毛四**

發佈日期： **11/08/2022 - 11/10/2022**

### 新功能 {#new-featres-264}

* 基礎架構更新，旨在縮短伺服器響應時間，提高系統的整體效能。
* 對新平台識別機制的改進。
* 能夠阻止來自SAML斷言中缺少&quot;in_response_to&quot;參數的MVPD的未經請求的身份驗證響應。

### 錯誤修復 {#bug-fixes-264}

* 已修復某些舊版TempPass令牌的錯誤格式。
* 已解決第二個螢幕身份驗證流上的次要問題。
