---
title: 自訂中繼資料
description: 自訂中繼資料
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 自訂中繼資料 {#custom-metadata}

**指定自訂索引鍵/值，以新增至伺服器應用程式可解譯的內容中繼資料。**

Adobe存取內容中繼資料格式允許在封裝時包含自訂金鑰/值配對，以便在授權發行期間由授權伺服器處理。 此中繼資料與原則不同，且每個內容片段可以唯一。

使用案例範例：在Beta版階段，您會在封裝時包含自訂屬性「Release：BETA」。 授權伺服器可以在Beta版期間購買此內容的授權，但在Beta版期間過期後，授權伺服器將不允許存取內容。
