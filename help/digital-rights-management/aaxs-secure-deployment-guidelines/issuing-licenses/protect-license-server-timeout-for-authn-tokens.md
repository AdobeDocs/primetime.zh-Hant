---
title: 驗證權杖的逾時
description: 驗證權杖的逾時
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 驗證權杖的逾時{#timeout-for-authentication-tokens}

Adobe存取SDK產生的所有驗證權杖都有保護應用程式安全的逾時間隔。 在處理驗證要求時，會使用Adobe存取SDK指定驗證權杖的到期日。 一旦過期後，驗證權杖就不再有效，使用者必須透過授權伺服器重新驗證。

若要深入瞭解驗證要求，請參閱 *Adobe存取API參考*.
