---
title: 部署證書
description: 部署證書
copied-description: true
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 部署證書{#deploy-certificates}

為避免在許可證伺服器上以明文形式提供PFX密碼，參考實現和Adobe PrimetimeDRM Server for Protected Streaming要求在配置檔案中指定時加密該密碼。 請參閱 *使用黃金時段DRM參考實現* 或 *使用黃金時段DRM伺服器* 以獲取有關運行加擾實用程式的說明。 其中每一個都包括其自己的擾碼實用程式，並且加密的密碼不能在這兩個許可證伺服器實現之間互換。

要將證書和加擾的密碼部署到您的許可證伺服器，請參閱 *使用黃金時段DRM參考實現* 或 *使用黃金時段DRM伺服器進行受保護的流處理*。
