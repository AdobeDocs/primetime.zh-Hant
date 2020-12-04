---
description: 檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。
seo-description: 檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。
seo-title: 內容與資訊清單需求
title: 內容與資訊清單需求
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 內容與資訊清單需求{#content-and-manifest-requirements}

檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。

| 在資訊清單檔案中，包含並設定每個ABR串流的`RESOLUTION`屬性。 您必須使用Flash Player 14或更新版本。 |
|---|
| 如果受DRM保護的流是多位速率(MBR)，則用於MBR的DRM加密密鑰應與所有位速率流中使用的密鑰相同。 |
| 必須與主要內容的轉譯具有相同的位元速率轉譯。 |