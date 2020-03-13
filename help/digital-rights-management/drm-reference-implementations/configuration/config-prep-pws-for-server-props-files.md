---
description: 'null'
seo-description: 'null'
seo-title: 為伺服器屬性檔案準備密碼
title: 為伺服器屬性檔案準備密碼
uuid: 3e00ba9b-b692-4713-8306-5ab896461f2a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 為伺服器屬性檔案準備密碼{#prepare-passwords-for-the-server-properties-files}

參考實作提 `ScrambleUtil.class`供一種類別，可確保憑證密碼的安全性。

在將密碼包含在檔案中之前，請使用此工具加密 [!DNL flashaccess-refimpl.properties] 密碼。

要運行該工具，可以使用Ant指令碼或Java。

該實用程式將生成加密口令，您必須將該口令複製到 [!DNL flashaccess-refimpl.properties] 檔案。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>已使用參考實作所 `ScrambleUtil.class` 提供之密碼進行編碼的密碼，不適用於Primetime DRM Server for Protected Streaming。
