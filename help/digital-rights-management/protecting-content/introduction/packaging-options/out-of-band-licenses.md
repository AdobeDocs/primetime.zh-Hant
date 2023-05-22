---
title: 帶外許可證
description: 帶外許可證
copied-description: true
exl-id: d9e54c8f-ff82-4834-a62e-20e67c4343dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 帶外許可證 {#out-of-band-licenses}

使用黃金時段DRM，您可以實現一個工作流，其中客戶端在帶外獲得預生成的許可證，因此無需部署許可證伺服器。 要支援此工作流，應在打包時指定一個選項，指明沒有可用的許可證伺服器。 這防止客戶端嘗試從許可證伺服器請求此內容的許可證。

指示許可證伺服器不可用的內容只能在Mogine DRM客戶端3.0版或更高版本上播放。 舊客戶端需要升級才能播放此內容。
