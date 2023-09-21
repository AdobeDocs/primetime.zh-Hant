---
title: 為伺服器屬性檔案準備密碼
description: 為伺服器屬性檔案準備密碼
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 為伺服器屬性檔案準備密碼{#prepare-passwords-for-the-server-properties-files}

參考實作提供 `ScrambleUtil.class`，確保認證密碼安全的類別。

在您將此密碼加入之前，請使用這個工具先加密密碼 [!DNL flashaccess-refimpl.properties] 檔案。

若要執行工具，您可以使用Ant指令碼或Java。

公用程式會產生加密的密碼，您必須將密碼複製到 [!DNL flashaccess-refimpl.properties] 檔案。

>[!NOTE]
>
>已使用編碼的密碼 `ScrambleUtil.class` 參考實作中提供的資料無法搭配Primetime DRM Server for Protected Streaming使用。
