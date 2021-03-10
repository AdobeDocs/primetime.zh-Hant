---
title: 重放保護
description: 重放保護
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 重放保護{#replay-protection}

重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶機的拒絕服務(DoS)攻擊（A *denial-of-service*&#x200B;攻擊是攻擊者試圖阻止服務的合法用戶使用該服務）。 例如，使用回滾計數器的重放攻擊可用於「誘騙」許可證伺服器，使其認為DRM客戶端正在回滾其狀態，導致帳戶暫停。

要瞭解有關重放保護的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*。`AbstractRequestMessage.getMessageId()`
