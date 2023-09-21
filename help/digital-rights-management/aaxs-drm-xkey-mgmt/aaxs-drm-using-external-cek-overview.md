---
description: 客戶可以使用Adobe存取(AAXS) DRM搭配自己的內容金鑰管理系統(CKMS)以及外部CEK功能。
title: Adobe存取DRM外部CEK概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Adobe存取DRM外部CEK概述 {#adobe-access-drm-external-cek-overview}

客戶可以使用Adobe存取(AAXS) DRM搭配自己的內容金鑰管理系統(CKMS)以及外部CEK功能。

Adobe存取(AAXS) DRM預設會抽象化在內容封裝過程中直接處理金鑰、憑證和DRM中繼資料的需求。 AAXS Java SDK會在封裝期間自動產生隨機內容加密金鑰(CEK)，並使用它來加密內容。 接下來，SDK會加密CEK本身，並將其插入內容的中繼資料中。 在授權發行時，AAXS伺服器只需要其AAXS授權伺服器私密金鑰即可從中繼資料存取CEK以產生授權。
