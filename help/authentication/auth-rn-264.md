---
title: Adobe Primetime authentication 2.64發行說明
description: Adobe Primetime authentication 2.64發行說明
exl-id: 4db21026-a0c2-4e33-b01f-4ccae824a110
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Adobe Primetime authentication 2.64發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考之用。 使用此API需要來自Adobe的目前授權。 不允許未經授權的使用。

本頁說明此版本的新功能、變更和已知問題：

## 伺服器端和Web使用者端 {#ss-web-clients}

* [建置編號](#build-no-264)
* [新功能](#new-featres-264)
* [錯誤修正](#bug-fixes-264)


### 建置編號 {#build-no-264}

Adobe Primetime驗證： adobe-pass-**2.64**

發行日期： **11/08/2022 - 11/10/2022**

### 新功能 {#new-featres-264}

* 基礎架構更新，旨在縮短伺服器回應時間，提升系統整體效能。
* 新平台識別機制的改良。
* 在SAML判斷提示中遺漏「in_response_to」引數的情況下，可封鎖來自MVPD的未經請求的驗證回應。

### 錯誤修正 {#bug-fixes-264}

* 修正部分舊版TempPass Token格式不正確的錯誤。
* 已解決第二個畫面驗證流程上的次要問題。
