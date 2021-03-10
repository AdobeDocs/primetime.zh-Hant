---
title: 自訂中繼資料
description: 自訂中繼資料
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 自訂中繼資料{#custom-metadata}

**指定自訂金鑰／值，以新增至可由伺服器應用程式解譯的內容中繼資料。**

Adobe存取內容中繼資料格式允許在封裝時包含自訂金鑰／值配對，以在授權發行期間由授權伺服器處理。 此中繼資料與原則不同，且對每個內容而言都是唯一的。

範例使用案例：在測試階段，您會在封裝時加入自訂屬性「Release:BETA」。 授權伺服器可在測試期間向此內容發放授權，但在測試期間到期後，授權伺服器就不允許存取內容。
