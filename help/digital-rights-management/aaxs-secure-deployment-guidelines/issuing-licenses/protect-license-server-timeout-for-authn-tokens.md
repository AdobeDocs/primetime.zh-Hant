---
title: 驗證Token逾時
description: 驗證Token逾時
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 驗證Token逾時{#timeout-for-authentication-tokens}

Adobe存取SDK產生的所有驗證Token都有保護應用程式安全的逾時間隔。 處理驗證請求時，會使用Adobe存取SDK指定驗證權杖的到期日。 到期過後，驗證權杖就不再有效，使用者必須透過授權伺服器重新驗證。

若要進一步瞭解驗證請求，請參閱 *Adobe存取API參考*.
