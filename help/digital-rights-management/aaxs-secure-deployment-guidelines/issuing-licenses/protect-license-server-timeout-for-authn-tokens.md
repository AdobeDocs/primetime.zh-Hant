---
title: 驗證令牌超時
description: 驗證令牌超時
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# 驗證令牌超時{#timeout-for-authentication-tokens}

Adobe訪問SDK生成的所有身份驗證令牌都有一個超時間隔，以保護應用程式安全。 在處理身份驗證請求時，使用Adobe訪問SDK指定身份驗證令牌的過期時間。 過期後，驗證令牌不再有效，用戶必須向許可證伺服器重新驗證。

要瞭解有關身份驗證請求的詳細資訊，請參閱 *Adobe訪問API參考*。
