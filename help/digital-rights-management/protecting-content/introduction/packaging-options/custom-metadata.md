---
title: 自訂中繼資料
description: 自訂中繼資料
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 自訂中繼資料{#custom-metadata}

使用它，將自訂金鑰／值配對新增至可由伺服器應用程式解譯的內容中繼資料。

Primetime DRM內容的中繼資料格式可讓您在封裝時加入自訂金鑰／值配對。 然後，授權伺服器可在授權發行期間處理此自訂中繼資料。 中繼資料與Primetime DRM政策不同，且對於每個內容區段而言都是唯一的。

範例使用案例：在測試階段，您可以在封裝時加入自訂屬性`Release:BETA`。 授權伺服器可在測試期間向此內容提供授權。 不過，在測試版期間過期後，授權伺服器就不允許存取內容。
