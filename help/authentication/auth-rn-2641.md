---
title: Adobe Primetime authentication 2.64.1發行說明
description: Adobe Primetime authentication 2.64.1發行說明
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Adobe Primetime authentication 2.64.1發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要Adobe的目前授權。 不允許未經授權的使用。

此頁面說明此版本的新功能、變更和已知問題：

## 伺服器端和Web使用者端 {#server-side-web-clients-2641}

* [建置編號](#build-number-2641)
* [版本總覽](#release-overview-2641)

### 建置編號 {#build-number-2641}

Adobe Primetime驗證： adobe-pass-**2.64.1**
發行日期： **01/31/2023 - 02/02/2023**

### 版本總覽 {#release-overview-2641}

此版本新增下列內容：

* 在SAML判斷提示中遺失「in_response_to」引數的情況下，封鎖來自MVPD的未經請求的驗證回應的功能。
* 已改善redirect_url引數的驗證，以符合安全性需求。
* 改善記錄第二熒幕驗證請求的裝置資訊，使用從初始裝置提供的資訊。
