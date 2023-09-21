---
title: 重播保護
description: 重播保護
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 重播保護{#replay-protection}

重播保護可防止攻擊者重播授權要求訊息，並可能對使用者端造成拒絕服務(DoS)攻擊(A) *拒絕服務* 攻擊是攻擊者嘗試阻止服務的合法使用者使用該服務。) 例如，使用倒回計數器的重播攻擊可能用來「誘騙」授權伺服器認為DRM使用者端正在倒回其狀態，導致帳戶暫停。

若要進一步瞭解重播保護，請參閱 `AbstractRequestMessage.getMessageId()` 此 *Adobe存取API參考*.
