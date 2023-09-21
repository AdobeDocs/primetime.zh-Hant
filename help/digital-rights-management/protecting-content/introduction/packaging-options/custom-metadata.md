---
title: 自訂中繼資料
description: 自訂中繼資料
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 自訂中繼資料 {#custom-metadata}

使用此項來將自訂索引鍵/值配對新增至伺服器應用程式可解譯的內容中繼資料。

Primetime DRM內容的中繼資料格式可讓您在封裝時包含自訂索引鍵/值配對。 然後，授權伺服器便可在授權發行期間處理此自訂中繼資料。 中繼資料與Primetime DRM政策不同，而且每個內容區段都可以是唯一的。

使用案例範例：在Beta版階段，您可以包含自訂屬性 `Release:BETA` 封裝時。 授權伺服器可以在Beta版期間銷售此內容的授權。 但是，在Beta版期限過期後，授權伺服器會禁止存取內容。
