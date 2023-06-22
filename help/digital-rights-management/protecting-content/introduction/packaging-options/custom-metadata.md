---
title: 自訂中繼資料
description: 自訂中繼資料
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 自訂中繼資料 {#custom-metadata}

使用此專案來將自訂索引鍵/值配對新增至可由伺服器應用程式解譯的內容中繼資料。

Primetime DRM內容的中繼資料格式可讓您在封裝時包含自訂索引鍵/值配對。 然後，授權伺服器便可在授權發行期間處理此自訂中繼資料。 中繼資料與Primetime DRM原則不同，而且每個內容區段都可獨特。

使用案例範例：在Beta版階段，您可以包含自訂屬性 `Release:BETA` 封裝時。 授權伺服器可以在Beta版期間發行此內容的授權。 但是，在Beta版期限過後，授權伺服器會禁止存取內容。
