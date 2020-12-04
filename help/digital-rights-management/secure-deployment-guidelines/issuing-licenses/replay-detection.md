---
description: 重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶端的拒絕服務(DoS)攻擊。
seo-description: 重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶端的拒絕服務(DoS)攻擊。
seo-title: 重放保護
title: 重放保護
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# 重放保護{#replay-protection}

重放保護可防止攻擊者重放許可證請求消息，並可能導致對客戶端的拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者試圖阻止服務的合法用戶使用該服務。 例如，使用回滾計數器的重放攻擊可用於「誘騙」許可證伺服器，使其認為DRM客戶端已回滾其狀態，從而導致帳戶暫停。

如需有關重放保護的詳細資訊，請參閱[ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId())。
