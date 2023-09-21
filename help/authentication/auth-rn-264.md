---
title: Adobe Primetime authentication 2.64發行說明
description: Adobe Primetime authentication 2.64發行說明
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# Adobe Primetime authentication 2.64發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

此頁面說明此版本的新功能、變更和已知問題：

## 伺服器端和Web使用者端 {#ss-web-clients}

* [建置編號](#build-no-264)
* [新功能](#new-featres-264)
* [錯誤修正](#bug-fixes-264)


### 建置編號 {#build-no-264}

Adobe Primetime驗證： adobe-pass-**2.64**

發行日期： **11/08/2022 - 11/10/2022**

### 新功能 {#new-featres-264}

* 基礎建設更新，旨在縮短伺服器回應時間，提升系統整體效能。
* 新平台識別機制的改進。
* 能夠封鎖來自MVPD的未經請求的驗證回應，其中SAML判斷提示中缺少&quot;in_response_to&quot;引數。

### 錯誤修正 {#bug-fixes-264}

* 修正部分舊版TempPass權杖格式不正確的問題。
* 已解決第二個畫面驗證流程上的次要問題。
