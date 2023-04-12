---
title: Adobe Primetime Authentication 2.64.1發行說明
description: Adobe Primetime Authentication 2.64.1發行說明
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Adobe Primetime Authentication 2.64.1發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面的內容僅供參考。 若要使用此API，必須具備目前的Adobe授權。 不允許未經授權使用。

本頁面說明此版本的新功能、變更和已知問題：

## 伺服器端和Web用戶端 {#server-side-web-clients-2641}

* [建置編號](#build-number-2641)
* [發行概述](#release-overview-2641)

### 建置編號 {#build-number-2641}

Adobe Primetime驗證：adobe-pass-**2.64.1**
發行日期： **01/31/2023 - 02/02/2023**

### 發行概述 {#release-overview-2641}

此版本新增下列內容：

* 能夠封鎖來自MVPD的未經請求的驗證回應，其中SAML斷言中缺少「in_response_to」參數。
* 改善redirect_url參數驗證，以符合安全性要求。
* 使用從初始設備提供的資訊改進了第二螢幕驗證請求的設備資訊的記錄。
