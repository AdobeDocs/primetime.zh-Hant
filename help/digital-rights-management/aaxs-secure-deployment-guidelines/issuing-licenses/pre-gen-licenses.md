---
title: 預先產生授權
description: 預先產生授權
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 預先產生授權{#pre-generating-licenses}

如果您要預先產生包含時間型使用規則的授權，強烈建議授權包含同步化需求(請參閱 *使用Adobe存取SDK保護內容* 指南)，以便安全地強制執行授權到期日。 如果您在授權中有任何以時間為基礎的限制，強烈建議在使用者端和伺服器之間實作「心率」機制，因為心率會將使用者端時間與伺服器時間同步。
