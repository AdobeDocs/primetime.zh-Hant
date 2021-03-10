---
description: 客戶可將Adobe存取(AAXS)DRM與其具有外部CEK功能的內容密鑰管理系統(CKMS)搭配使用。
title: Adobe存取DRM外部CEK概觀
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Adobe訪問DRM外部CEK概述{#adobe-access-drm-external-cek-overview}

客戶可將Adobe存取(AAXS)DRM與其具有外部CEK功能的內容密鑰管理系統(CKMS)搭配使用。

Adobe存取(AAXS)DRM依預設會抽象出在內容封裝程式中直接處理金鑰、憑證和DRM中繼資料的需求。 AAXS Java SDK會在封裝期間自動產生隨機內容加密金鑰(CEK)，並使用它來加密內容。 接著SDK會加密CEK本身，並將其插入內容的中繼資料。 在授權發行時，AAXS伺服器只需要其AAXS授權伺服器私密金鑰，才能從中繼資料存取CEK以產生授權。
