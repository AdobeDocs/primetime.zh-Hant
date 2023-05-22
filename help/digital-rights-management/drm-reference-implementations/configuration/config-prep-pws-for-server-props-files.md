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

參考實現提供 `ScrambleUtil.class`，一個可確保憑據密碼安全性的類。

在將密碼包含到 [!DNL flashaccess-refimpl.properties] 的子菜單。

要運行該工具，可以使用Ant指令碼或Java。

該實用程式將生成加密密碼，您必須將其複製到 [!DNL flashaccess-refimpl.properties] 的子菜單。

>[!NOTE]
>
>已與 `ScrambleUtil.class` 已提供的參考實現與Mogfire DRM Server for Protected Streaming不相容。
