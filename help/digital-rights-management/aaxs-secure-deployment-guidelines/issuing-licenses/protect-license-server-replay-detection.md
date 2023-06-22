---
title: 重播保護
description: 重播保護
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 重播保護{#replay-protection}

重播保護可防止攻擊者重播授權要求訊息，並可能對使用者端造成拒絕服務(DoS)攻擊(A) *拒絕服務* 攻擊是攻擊者試圖阻止服務的合法使用者使用該服務的行為。) 例如，使用倒回計數器的重播攻擊可能用來「誘騙」License Server認為DRM使用者端正在倒回其狀態，導致帳戶暫停。

若要進一步瞭解重播保護，請參閱 `AbstractRequestMessage.getMessageId()` 此 *Adobe存取API參考*.
