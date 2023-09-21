---
title: 撤銷使用者端認證
description: 撤銷使用者端認證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 撤銷使用者端認證{#revoking-client-credentials}

在某些情況下，必須撤銷使用者端的認證，或檢查指定的認證集是否已撤銷。 如果認證遭到破壞，認證可能會被撤銷。 發生此情況時，將不再核發授權給受影響的使用者端。

Adobe會維護憑證撤銷清單(CRL)，以撤銷受到危害的使用者端。 SDK會自動強制執行這些CRL。 授權伺服器可能會禁止特定機器認證或DRM和執行階段認證的特定版本，進而限制使用者端。 A `RevocationList` 可能會建立並傳遞至SDK，以撤銷電腦認證。 特定DRM/執行階段版本可在原則層級（透過在播放許可權中設定模組限制）或全域（透過在設定模組限制）撤銷 `HandlerConfiguration`)。

本章的討論將集中於撤銷使用者端憑證。
