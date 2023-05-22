---
title: 遠程和本地iOS密鑰交付
description: 遠程和本地iOS密鑰交付
copied-description: true
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 遠程和本地iOS密鑰交付 {#remote-and-local-ios-key-delivery}

Adobe Primetime支援以下選項，用於向iOS客戶提供關鍵交付：

* **遠程**  — 按照HTTP即時流(HLS)規範中的指定執行；M3U8清單指定HTTPS路徑，該路徑包括應用於解密流中以下加密段的AES密鑰。 指定時 `Remote` 在黃金時段DRM策略中，客戶端設備必須連接到遠程HTTPS伺服器以獲取AES密鑰。

* **本地**  — 指定時 `Local` 在黃金時段DRM中，本地HTTPS伺服器被嵌入到iOS應用程式中，然後該應用程式管理所有AES密鑰請求，而不是連接到網際網路/網路以獲取AES密鑰。 嵌入式HTTPS伺服器在P應用程式中自動設定和配置。 應用程式開發人員不需要干預。

遠程密鑰傳遞通過用於包裝內容的黃金時段DRM策略啟用。 如果要更改此設定，必須重新打包內容。 如果啟用遠程密鑰傳遞，則必須部署一個Mogifle DRM密鑰伺服器，該伺服器可以管理來自iOS客戶端的密鑰請求。 但是，其他平台上客戶端的工作流沒有更改。

>[!NOTE]
>
>密鑰傳遞選擇僅影響iOS客戶端。 使用HLS內容的所有其他設備，如Android和Mighide on Desktop(Flash Player)，始終使用 `Local` 鍵傳遞，即使 `Remote` 已指定。
