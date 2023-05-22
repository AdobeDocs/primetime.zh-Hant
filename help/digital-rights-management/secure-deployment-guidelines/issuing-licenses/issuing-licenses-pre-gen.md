---
description: 如果預生成包含基於時間的使用規則的許可證，則許可證應包括同步要求，以安全地強制實施許可證到期。
title: 預生成許可證
exl-id: f3b6927d-66cf-4aa2-802d-d4b3a5652c63
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 預生成許可證{#pre-generating-licenses}

如果預生成包含基於時間的使用規則的許可證，則許可證應包括同步要求，以安全地強制實施許可證到期。

如果許可證中存在任何基於時間的限制，則在客戶端和伺服器之間實施「心跳」機制有助於將客戶端時間與伺服器時間同步。

有關詳細資訊，請參見 [使用Adobe PrimetimeDRM SDK保護內容](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf)。
