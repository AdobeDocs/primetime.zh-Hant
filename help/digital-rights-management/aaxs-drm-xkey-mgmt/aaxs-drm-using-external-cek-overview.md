---
description: 客戶可以使用Adobe訪問(AAXS)DRM和其自己的內容密鑰管理系統(CKMS)和外部CEK功能。
title: Adobe訪問DRM外部CEK概述
exl-id: 4131863b-5773-4222-aae9-d984267cdb86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Adobe訪問DRM外部CEK概述 {#adobe-access-drm-external-cek-overview}

客戶可以使用Adobe訪問(AAXS)DRM和其自己的內容密鑰管理系統(CKMS)和外部CEK功能。

Adobe訪問(AAXS)DRM預設表示在內容打包過程中直接處理密鑰、證書和DRM元資料的需要。 AAXS Java SDK將在打包期間自動生成隨機內容加密密鑰(CEK)，並使用它加密內容。 接下來，SDK會加密CEK本身，並將其插入內容的元資料中。 在許可證發放時，AAXS伺服器只需要其AAXS許可證伺服器私鑰即可從元資料存取CEK以生成許可證。
