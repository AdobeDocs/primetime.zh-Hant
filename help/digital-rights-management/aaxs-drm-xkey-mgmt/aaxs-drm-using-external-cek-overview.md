---
description: 客戶可搭配使用Adobe Access(AAXS)DRM和其內容金鑰管理系統(CKMS)及外部CEK功能。
seo-description: 客戶可搭配使用Adobe Access(AAXS)DRM和其內容金鑰管理系統(CKMS)及外部CEK功能。
seo-title: Adobe Access DRM External CEK概觀
title: Adobe Access DRM External CEK概觀
uuid: ea0bba63-7743-4216-863f-392500998eb6
translation-type: tm+mt
source-git-commit: 92e04cbb5e94f60c8d06e94b826ff9361c10ef97
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Adobe Access DRM External CEK概觀{#adobe-access-drm-external-cek-overview}

客戶可搭配使用Adobe Access(AAXS)DRM和其內容金鑰管理系統(CKMS)及外部CEK功能。

Adobe Access(AAXS)DRM依預設會摘要說明在內容封裝程式中，直接處理金鑰、憑證和DRM中繼資料的需求。 AAXS Java SDK會在封裝期間自動產生隨機內容加密金鑰(CEK)，並使用它來加密內容。 接著SDK會加密CEK本身，並將其插入內容的中繼資料。 在授權發行時，AAXS伺服器只需要其AAXS授權伺服器私密金鑰，才能從中繼資料存取CEK以產生授權。
