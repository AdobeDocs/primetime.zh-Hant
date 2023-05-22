---
title: Adobe Primetime身份驗2.64.1發行說明
description: Adobe Primetime身份驗2.64.1發行說明
exl-id: b0edbd90-ebb5-40a7-9034-1699dccfadb5
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Adobe Primetime身份驗2.64.1發行說明 {#authn-264-rn}

>[!NOTE]
>
>此頁面上的內容僅供參考。 使用此API需要來自Adobe的當前許可證。 不允許未經授權使用。

本頁介紹此版本的新功能、更改和已知問題：

## 伺服器端和Web客戶端 {#server-side-web-clients-2641}

* [內部版本號](#build-number-2641)
* [發行概述](#release-overview-2641)

### 內部版本號 {#build-number-2641}

Adobe Primetime驗證：adobe-pass-**2.64.1**
發佈日期： **01/31/2023 - 02/02/2023**

### 發行概述 {#release-overview-2641}

此版本添加了以下內容：

* 能夠阻止來自SAML斷言中缺少&quot;in_response_to&quot;參數的MVPD的未經請求的身份驗證響應。
* 通過redirect_url參數改進的驗證，以符合安全性要求。
* 使用從初始設備提供的資訊改進記錄用於第二螢幕驗證請求的設備資訊。
