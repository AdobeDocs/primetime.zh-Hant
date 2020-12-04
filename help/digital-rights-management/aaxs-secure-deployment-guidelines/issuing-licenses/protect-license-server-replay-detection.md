---
seo-title: 重放保護
title: 重放保護
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 重放保護{#replay-protection}

重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶機的拒絕服務(DoS)攻擊（A *denial-of-service*&#x200B;攻擊是攻擊者試圖阻止服務的合法用戶使用該服務）。 例如，使用回滾計數器的重放攻擊可用於「誘騙」許可證伺服器，使其認為DRM客戶端正在回滾其狀態，導致帳戶暫停。

若要進一步瞭解重放保護，請參閱`AbstractRequestMessage.getMessageId()`Adobe Access API參考&#x200B;*。*
