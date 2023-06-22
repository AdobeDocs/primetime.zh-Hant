---
title: 頻外授權
description: 頻外授權
copied-description: true
exl-id: d9e54c8f-ff82-4834-a62e-20e67c4343dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 頻外授權 {#out-of-band-licenses}

使用Primetime DRM，您可以實作一個工作流程，讓使用者端在頻外取得預先產生的授權，因此無需部署授權伺服器。 若要支援此工作流程，封裝時應指定表示沒有可用的授權伺服器選項。 這可防止使用者端嘗試從授權伺服器要求此內容的授權。

指出許可證伺服器無法使用狀態的內容只能在Primetime DRM使用者端3.0版或更新版本上播放。 舊版使用者端需要升級才能播放此內容。
