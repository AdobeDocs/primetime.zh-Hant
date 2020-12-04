---
seo-title: 預先產生的授權
title: 預先產生的授權
uuid: 0207abdf-52bb-4bd0-a4f2-fe740b89fa83
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 預先產生授權{#pre-generating-licenses}

如果您預先產生包含時間型使用規則的授權，強烈建議授權包含同步要求（請參閱&#x200B;*使用Adobe Access SDK for Protecting Content*&#x200B;指南），以安全地強制授權到期。 如果您在授權中有任何時間限制，強烈建議在用戶端與伺服器之間實作「心拍」機制，因為心拍會同步用戶端的時間與伺服器時間。
