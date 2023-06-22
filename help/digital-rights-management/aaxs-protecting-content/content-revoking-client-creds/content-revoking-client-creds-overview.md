---
title: 撤銷使用者端認證
description: 撤銷使用者端認證
copied-description: true
exl-id: 583dff28-c34a-4759-81a6-0471feab309f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 撤銷使用者端認證{#revoking-client-credentials}

在某些情況下，必須撤銷使用者端的認證，或檢查指定的認證集是否已撤銷。 如果認證遭到破壞，認證可能會被撤銷。 發生此情況時，將不再核發授權給受影響的使用者端。

Adobe會維護可撤銷受威脅使用者端的憑證撤銷清單(CRL)。 SDK會自動強制執行這些CRL。 授權伺服器可能會禁止特定機器認證或DRM和執行階段認證的特定版本，進而限制使用者端。 A `RevocationList` 可建立並傳遞至SDK以撤銷電腦認證。 特定DRM/執行階段版本可以在原則層級（透過在播放許可權中設定模組限制）或全域（透過在設定模組限制）撤銷 `HandlerConfiguration`)。

本章的討論內容將集中於撤銷使用者端憑證。
