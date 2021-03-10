---
title: 驗證Token的逾時
description: 驗證Token的逾時
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# 驗證Token的逾時{#timeout-for-authentication-tokens}

所有由Adobe存取SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。 在處理驗證要求時，會使用Adobe存取SDK來指定驗證Token的有效期。 一旦過期，驗證Token就不再有效，使用者必須向授權伺服器重新驗證。

若要進一步瞭解驗證請求，請參閱&#x200B;*Adobe存取API參考*&#x200B;中的AuthenticationHandler。
