---
title: Adobe Primetime authentication 2.64發行說明
description: Adobe Primetime authentication 2.64發行說明
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Adobe Primetime authentication 2.64發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

本頁面說明此版本的新功能、變更和已知問題：

## 伺服器端和Web用戶端 {#ss-web-clients}

* [建置編號](#build-no-264)
* [新功能](#new-featres-264)
* [錯誤修正](#bug-fixes-264)


### 建置編號 {#build-no-264}

Adobe Primetime驗證：adobe-pass-**2.64**

發行日期： **11/08/2022 - 11/10/2022**

### 新功能 {#new-featres-264}

* 基礎架構更新，旨在縮短伺服器響應時間，提高系統的整體效能。
* 對新平台識別機制的改進。
* 能夠封鎖來自MVPD的未經請求的驗證回應，其中SAML斷言中缺少「in_response_to」參數。

### 錯誤修正 {#bug-fixes-264}

* 修正某些舊版TempPass代號的格式錯誤。
* 已解決第二個螢幕驗證流程的次要問題。
