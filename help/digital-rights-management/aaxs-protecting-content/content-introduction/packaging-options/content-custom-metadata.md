---
title: 自定義元資料
description: 自定義元資料
copied-description: true
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 自定義元資料 {#custom-metadata}

**指定自定義鍵/值，以添加到可由伺服器應用程式解釋的內容元資料中。**

Adobe訪問內容元資料格式允許在打包時包含定製密鑰/值對，以在許可證簽發期間由許可證伺服器處理。 此元資料與策略分開，對於每個內容都可以是唯一的。

示例用例：在Beta階段，您在打包時包括自定義屬性「Release:BETA」。 許可證伺服器可以在試用期內向此內容提供許可證，但在試用期到期後，許可證伺服器將不允許訪問該內容。
