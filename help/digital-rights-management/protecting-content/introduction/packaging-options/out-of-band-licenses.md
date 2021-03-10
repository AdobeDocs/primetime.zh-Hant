---
title: 帶外授權
description: 帶外授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 帶外許可證{#out-of-band-licenses}

使用Primetime DRM，您可以實作客戶端在帶外取得預先產生之授權的工作流程，因此毋需部署授權伺服器。 若要支援此工作流程，應在封裝時指定指示沒有可用的授權伺服器選項。 這可防止客戶端嘗試向許可證伺服器請求此內容的許可證。

表示授權伺服器不可用的內容只能在Primetime DRM用戶端3.0版或更新版本上播放。 較舊的客戶需要升級才能播放此內容。
