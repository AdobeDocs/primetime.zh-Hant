---
description: 檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。
title: 內容與資訊清單需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# 內容與資訊清單需求{#content-and-manifest-requirements}

檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。

| 在資訊清單檔案中，包含並設定每個ABR串流的`RESOLUTION`屬性。 您必須使用Flash Player14或更新版本。 |
|---|
| 如果受DRM保護的流是多位速率(MBR)，則用於MBR的DRM加密密鑰應與所有位速率流中使用的密鑰相同。 |
| 必須與主要內容的轉譯具有相同的位元速率轉譯。 |