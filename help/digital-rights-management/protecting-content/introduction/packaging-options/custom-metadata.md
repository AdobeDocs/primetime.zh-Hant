---
title: 自定義元資料
description: 自定義元資料
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 自定義元資料 {#custom-metadata}

使用此選項可將自定義鍵/值對添加到可由伺服器應用程式解釋的內容元資料中。

使用黃金時段DRM內容的元資料格式，您可以在打包時包括自定義密鑰/值對。 然後，許可證伺服器可以在許可證簽發期間處理此自定義元資料。 元資料與黃金時段DRM策略分開，並且對於每個內容部分是唯一的。

示例用例：在Beta階段，您可以包括自定義屬性 `Release:BETA` 打包時。 許可證伺服器可以在試用期內向此內容提供許可證。 但是，在Beta期過後，許可證伺服器不允許訪問內容。
