---
description: 多CDN允許設定一個或多個CDN位置以服務轉碼廣告。
title: 多CDN支援
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 多CDN支援 {#multi-cdn-support}

多CDN允許設定一個或多個CDN位置以服務轉碼廣告。

預設情況下，所有轉碼資產都托管在Adobe擁有的Akamai CDN上。 但是，您可以選擇您自己的零個或多個附加CDN位置，CRS將在其中托管已轉碼資產。 因此，在這種情況下，您的轉碼資產和內容可以從同一CDN提供。

當清單伺服器對轉碼請求進行查找時，它使用包含多個查詢參數的引導URL。 如果已設定多CDN環境，則引導URL還需要包含 `ptcdn` parameter.清單伺服器使用此參數來標識從中獲取轉碼版本的CDN伺服器。

Multi CDN支援還可用於以下黃金時段解決方案：

1. 用於Android的TVSDK
1. 用於案頭HLS的TVSDK
1. iOSTVSDK

## 啟用CDN支援 {#section_1BA344F2300B49F291865A7461EDFEAE}

預設情況下，CRS為所有客戶禁用

請與Adobe技術帳戶經理聯繫，以配置您的CRS帳戶以使用其他CDN來托管轉碼廣告資產。您需要提供CRS將轉碼廣告資產上載到CDN所需的以下資訊

1. CDN URL
1. 身份驗證詳細資訊
1. 輸出URL格式

此外，您的Adobe技術客戶經理將為您提供此CDN的暱稱。您需要將此暱稱作為 `ptcdn` 的子菜單。

您可以通過Adobe支援在CRS端配置多個CDN。 但是，用於挑選要通過清單伺服器縫合的廣告資產的CDN必須是作為 `ptcdn` 的子菜單。
