---
title: 重放保護
description: 重放保護
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 重放保護{#replay-protection}

重播保護防止攻擊者重播許可證請求消息，並可能導致對客戶端的拒絕服務(DoS)攻擊(A) *拒絕服務* 攻擊是攻擊者試圖阻止服務的合法用戶使用該服務。) 例如，使用回滾計數器的重播攻擊可用於「欺騙」許可證伺服器，使其認為DRM客戶端正在回滾其狀態，從而導致帳戶暫停。

要瞭解有關重播保護的詳細資訊，請參見 `AbstractRequestMessage.getMessageId()` 這樣 *Adobe訪問API參考*。
