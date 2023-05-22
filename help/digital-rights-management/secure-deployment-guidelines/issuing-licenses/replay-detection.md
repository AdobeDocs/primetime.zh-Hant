---
description: 重播保護可防止攻擊者重放許可證請求消息，並可能對客戶端造成拒絕服務(DoS)攻擊。
title: 重放保護
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 重放保護{#replay-protection}

重播保護可防止攻擊者重放許可證請求消息，並可能對客戶端造成拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者試圖阻止服務的合法用戶使用該服務。 例如，使用回滾計數器的重播攻擊可用於「欺騙」許可證伺服器，使其認為DRM客戶端已回滾其狀態，從而導致帳戶暫停。

要瞭解有關重播保護的詳細資訊，請參見 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。
