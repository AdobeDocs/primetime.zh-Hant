---
description: 檢查串流和播放清單（資訊清單）的限制和需求，包括DRM加密金鑰。
title: 內容和資訊清單需求
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 內容和資訊清單需求 {#content-and-manifest-requirements}

檢查串流和播放清單（資訊清單）的限制和需求，包括DRM加密金鑰。

| 包含並設定 `RESOLUTION` 資訊清單檔案中每個ABR資料流的屬性。 您必須使用Flash Player14或更新版本。 |
|---|
| 如果受DRM保護的資料流是多位元速率(MBR)，則用於MBR的DRM加密金鑰應與所有位元速率資料流中使用的金鑰相同。 |
| 必須與主要內容的轉譯具有相同位元速率轉譯。 |
