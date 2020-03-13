---
seo-title: 驗證Token的逾時
title: 驗證Token的逾時
uuid: 41b0fbf5-a567-4118-bec1-c05e6e0b6d1f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 驗證Token的逾時{#timeout-for-authentication-tokens}

Adobe Access SDK產生的所有驗證Token都有逾時間隔，以保護應用程式的安全性。 在處理驗證要求時，會使用Adobe Access SDK來指定驗證Token的有效期。 一旦過期，驗證Token就不再有效，使用者必須向授權伺服器重新驗證。

若要進一步瞭解驗證要求，請參閱 *Adobe Access API參考中的AuthenticationHandler*。
