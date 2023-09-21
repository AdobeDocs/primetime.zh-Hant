---
title: 非對稱金鑰加密
description: 非對稱金鑰加密
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 非對稱金鑰加密{#asymmetric-key-encryption}

非對稱金鑰加密（也稱為公開金鑰加密）使用金鑰組。 其中一個金鑰用於加密，另一個用於解密。 解密金鑰是保密的，稱為 *私密金鑰*. 加密金鑰，稱為 *公開金鑰*，可供任何獲授權加密內容的人使用。 有權存取公開金鑰的人員都可以加密內容，但只有有權存取私密金鑰的人員才能解密內容。 無法從公開金鑰重建私密金鑰。

封裝內容時，會使用授權伺服器的公開金鑰來加密DRM中繼資料中的內容加密金鑰(CEK)。 您必須確保只有License Server可以存取License Server的私密金鑰；如果其他人擁有該金鑰，他們可以解密並檢視內容。

***注意：**請確定您是從信任的來源取得License Server的憑證（包含公開金鑰），因此您可以確定該憑證是License Server的金鑰，而不是惡意公開金鑰。 如果攻擊者用他們的公開金鑰取代授權伺服器的金鑰，他們將能夠解密您的內容。*

如需封裝內容的詳細資訊，請參閱 *使用Adobe Access SDK保護內容*.
