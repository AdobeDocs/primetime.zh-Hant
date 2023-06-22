---
title: 為伺服器屬性檔案準備密碼
description: 為伺服器屬性檔案準備密碼
copied-description: true
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 為伺服器屬性檔案準備密碼{#prepare-passwords-for-the-server-properties-files}

參考實作提供 `ScrambleUtil.class`，確保認證密碼安全的類別。

在密碼加入之前，請使用此工具先加密密碼 [!DNL flashaccess-refimpl.properties] 檔案。

若要執行工具，您可以使用Ant指令碼或Java。

公用程式會產生加密的密碼，您必須將密碼複製到 [!DNL flashaccess-refimpl.properties] 檔案。

>[!NOTE]
>
>密碼已使用 `ScrambleUtil.class` 參考實作中提供的資料無法搭配Primetime DRM伺服器使用，因此無法進行受保護的串流。
