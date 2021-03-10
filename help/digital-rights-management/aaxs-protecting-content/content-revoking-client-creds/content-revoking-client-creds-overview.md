---
title: 廢止用戶端認證
description: 廢止用戶端認證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 廢止用戶端認證{#revoking-client-credentials}

在某些情況下，必須撤銷客戶端的憑據，或檢查給定的一組憑據是否已被撤銷。 如果證書受到危害，則可撤銷證書。 發生此情況時，授權將不再發給受損客戶。

Adobe會維護「證書撤銷清單」(CRL)，以撤銷受危害的客戶。 這些CRL由SDK自動執行。 許可伺服器可以通過禁止特定電腦認證或特定版本的DRM和運行時認證進一步限制客戶端。 可以建立`RevocationList`並傳入SDK以廢止電腦憑證。 特定的DRM/執行時期版本可以在策略級別（通過在播放權中設定模組限制）或全局（通過在`HandlerConfiguration`中設定模組限制）撤銷。

本章中的討論將集中在廢止用戶端認證上。
