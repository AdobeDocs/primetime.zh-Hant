---
description: 'null'
seo-description: 'null'
seo-title: 為伺服器屬性檔案準備密碼
title: 為伺服器屬性檔案準備密碼
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 為伺服器屬性檔案準備密碼{#prepare-passwords-for-the-server-properties-files}

參考實作提供`ScrambleUtil.class`，此類可確保憑證密碼的安全性。

在將密碼包含在[!DNL flashaccess-refimpl.properties]檔案中之前，請使用此工具加密該密碼。

要運行該工具，可以使用Ant指令碼或Java。

該實用程式生成加密口令，您必須將該口令複製到[!DNL flashaccess-refimpl.properties]檔案。

>[!NOTE]
>
>已使用`ScrambleUtil.class`編碼的密碼（已隨參考實作提供）不適用於Primetime DRM Server for Protected Streaming。
