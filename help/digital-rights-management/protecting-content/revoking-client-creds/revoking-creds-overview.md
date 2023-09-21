---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概觀{#overview}

您可能需要撤銷使用者端的認證，或檢查指定的認證集是否已在某些情況下被撤銷。 如果認證受到危害，則可撤銷認證。 當這些問題發生時，授權將不再核發給受影響的使用者端。

Adobe會維護憑證撤銷清單(CRL)，以撤銷受到危害的使用者端。 SDK會自動強制執行這些CRL。 授權伺服器可能會禁止特定機器認證或DRM和執行階段認證的特定版本，進而限制使用者端。 A `RevocationList` 可能會建立並傳遞至SDK，以撤銷電腦認證。 您可以在DRM原則層級撤銷特定DRM/執行階段版本，方法是在播放許可權中設定模組限制，或是在中設定模組限制 `HandlerConfiguration`.

討論的焦點是撤銷使用者端憑證。
