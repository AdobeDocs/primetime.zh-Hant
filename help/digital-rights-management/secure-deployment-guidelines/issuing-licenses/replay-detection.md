---
description: 重播保護可防止攻擊者重播授權要求訊息，並可能對使用者端造成拒絕服務(DoS)攻擊。
title: 重播保護
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 重播保護{#replay-protection}

重播保護可防止攻擊者重播授權要求訊息，並可能對使用者端造成拒絕服務(DoS)攻擊。

DoS攻擊是攻擊者嘗試阻止服務的合法使用者使用該服務的行為。 例如，使用倒回計數器的重播攻擊可能用來「誘騙」License Server認為DRM使用者端已倒回其狀態，進而導致帳戶暫停。

若要進一步瞭解重播保護，請參閱 [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
