---
title: 預生成許可證
description: 預生成許可證
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 預生成許可證{#pre-generating-licenses}

如果您是預生成包含基於時間的使用規則的許可證，強烈建議該許可證包括同步要求(請參閱 *使用Adobe訪問SDK保護內容* 指南)，因此可以安全地強制執行許可證過期。 如果您在許可證中有任何基於時間的限制，強烈建議在客戶端和伺服器之間實施「心跳」機制，因為心跳將使客戶端時間與伺服器時間同步。
