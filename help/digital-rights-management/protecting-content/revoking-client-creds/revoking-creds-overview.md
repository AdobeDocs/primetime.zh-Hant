---
title: 概觀
description: 概觀
copied-description: true
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概觀{#overview}

您可能需要撤銷使用者端的認證，或檢查指定的認證集是否已在某些情況下被撤銷。 如果認證受到危害，可能會遭撤銷。 當這些問題發生時，授權將不再核發給受影響的使用者端。

Adobe會維護可撤銷受威脅使用者端的憑證撤銷清單(CRL)。 SDK會自動強制執行這些CRL。 授權伺服器可能會禁止特定機器認證或DRM和執行階段認證的特定版本，進而限制使用者端。 A `RevocationList` 可建立並傳遞至SDK以撤銷電腦認證。 您可以在DRM原則層級，透過在播放權中設定模組限制來撤銷特定DRM/執行階段版本，或透過在設定模組限制來全域撤銷特定DRM/執行階段版本。 `HandlerConfiguration`.

討論的焦點是撤銷使用者端憑證。
