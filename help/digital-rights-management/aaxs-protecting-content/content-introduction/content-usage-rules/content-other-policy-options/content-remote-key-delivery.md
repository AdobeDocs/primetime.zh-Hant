---
title: 遠程和本地iOS密鑰交付
description: 遠程和本地iOS密鑰交付
copied-description: true
exl-id: de9c7070-46a9-453c-9d98-a9f161282cfa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 遠程和本地iOS密鑰交付{#remote-and-local-ios-key-delivery}

Adobe Primetime支援兩種將密鑰交付給iOS客戶的選項：

* Remote — 與HLS規範中指定的完全一樣，M3U8清單指定了一個HTTPS路徑，該路徑包含一個AES密鑰，該密鑰應用於解密流中的以下加密段。 指定「遠程」時，客戶端設備將訪問遠程HTTPS伺服器以獲取AES密鑰。
* 本地 — 當指定「本地」時，本地HTTPS伺服器將嵌入到iOS應用程式中，該應用程式將處理所有AES密鑰請求。 嵌入式HTTPS伺服器在Mogfire應用程式中自動設定和配置。 應用程式開發人員不需要干預。

通過用於打包內容的策略啟用遠程密鑰傳遞（更改此設定需要重新打包內容）。啟用遠程密鑰傳遞後，必須部署Adobe訪問密鑰伺服器來處理來自iOS客戶端的密鑰請求，但對其他平台上的客戶端的工作流沒有更改。

>[!NOTE]
>
>密鑰傳遞選擇僅影響iOS客戶端。 使用HLS內容的所有其它設備將始終使用「本地」密鑰傳遞，即使已指定「遠程」。

有關資訊，請參見 *使用Adobe訪問密鑰伺服器*。
