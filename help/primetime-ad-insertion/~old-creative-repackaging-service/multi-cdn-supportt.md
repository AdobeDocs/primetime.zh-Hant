---
description: Multi CDN允許設定一或多個CDN位置，以提供轉碼廣告。
title: 多CDN支援
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 多CDN支援{#multi-cdn-support}

Multi CDN允許設定一或多個CDN位置，以提供轉碼廣告。

依預設，所有轉碼資產都會托管在Adobe擁有的Akamai CDN上。 不過，您可以選擇您自己的零個或多個額外CDN位置，CRS將在此處裝載轉碼資產。 因此，在此案例中，您的轉碼資產和內容可從相同的CDN提供。

當資訊清單伺服器對轉碼請求進行查詢時，會使用包含許多查詢參數的引導URL。 如果您已設定多CDN環境，啟動載入URL也需要包含`ptcdn`參數。manifest伺服器會使用此參數來識別要從中取得轉碼版本廣告的CDN伺服器。

Primetime解決方案也支援多CDN:

1. Android專用的TVSDK
1. Desktop HLS的TVSDK
1. iOS版TVSDK

## 啟用CDN支援{#section_1BA344F2300B49F291865A7461EDFEAE}

依預設，CRS會針對所有客戶停用

請連絡您的Adobe技術帳戶管理員，以設定您的CRS帳戶以使用其他CDN來代管轉碼廣告資產。您必須提供下列CRS將轉碼廣告資產上傳至CDN所需的資訊

1. CDN URL
1. 驗證詳細資訊
1. 輸出URL格式

此外，您的Adobe技術客戶經理將為您提供此CDN的暱稱。您必須將此名稱傳入BootstrapURL中作為`ptcdn`參數的值。

您可以透過Adobe支援在CRS端設定多個CDN。 不過，用於挑選透過資訊清單伺服器銜接的廣告資產的CDN必須是作為BootstrapURL中`ptcdn`參數值傳遞的CDN。
