---
description: Multi CDN允許設定一或多個CDN位置以提供轉碼廣告。
title: 多CDN支援
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 多CDN支援 {#multi-cdn-support}

Multi CDN允許設定一或多個CDN位置以提供轉碼廣告。

依預設，所有轉碼資產都由Adobe擁有的Akamai CDN代管。 不過，您可以自行選擇零個或多個其他CDN位置，讓CRS代管轉碼資產。 因此，在此情況下，您可以從相同的CDN提供轉碼資產和內容。

資訊清單伺服器查詢轉碼請求時，會使用包含許多查詢引數的啟動程式URL。 如果您已設定多CDN環境，啟動程式URL也需要包含 `ptcdn` parameter.資訊清單伺服器會使用此引數來識別要從中取得轉碼版廣告的CDN伺服器。

下列Primetime解決方案也提供多CDN支援：

1. 適用於Android的TVSDK
1. 適用於案頭HLS的TVSDK
1. 適用於iOS的TVSDK

## 啟用CDN支援 {#section_1BA344F2300B49F291865A7461EDFEAE}

預設情況下，所有客戶的CRS皆停用

請聯絡您的Adobe技術客戶經理，設定您的CRS帳戶以使用其他CDN來託管轉碼廣告資產。您將需要提供CRS上傳轉碼廣告資產至CDN所需的下列資訊

1. CDN URL
1. 驗證詳細資料
1. 輸出URL格式

此外，您的Adobe技術客戶經理將為您提供此CDN的暱稱。您需要將此作為 `ptcdn` BootstrapURL中的引數。

您可以透過Adobe支援，在CRS端上設定多個CDN。 不過，用來挑選要透過資訊清單伺服器連結的廣告資產的CDN，必須傳遞為的值 `ptcdn` BootstrapURL中的引數。
