---
title: 預先產生的授權
description: 預先產生的授權
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# 預先產生授權{#pre-generating-licenses}

如果您預先產生包含時間型使用規則的授權，強烈建議授權包含同步要求(請參閱&#x200B;*使用Adobe存取SDK以保護內容*&#x200B;指南)，以便安全地強制授權到期。 如果您在授權中有任何時間限制，強烈建議在用戶端和伺服器之間實作「心搏」機制，因為心搏會同步用戶端的時間與伺服器時間。
