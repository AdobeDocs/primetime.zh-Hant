---
description: 所有廣告插入請求都使用相同的URL結構和相同的基本查詢參數。 額外的查詢參數可讓資訊清單伺服器搭配各種用戶端和情況運作。
title: 廣告插入請求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 廣告插入請求{#requests-for-ad-insertion}

所有廣告插入請求都使用相同的URL結構和相同的基本查詢參數。 額外的查詢參數可讓資訊清單伺服器搭配各種用戶端和情況運作。

| 參數 | 說明 |
|--- |--- |
| u | 資產ID是來自Adobe Primetime廣告決策中繼資料的ad_request_id的MD5雜湊。 由您的Adobe技術客戶經理提供。 |
| z | 必須提供給Auditude之資產的區域ID。 由您的Adobe技術客戶經理提供。 |
| `__sid__` | 資訊清單伺服器將用來產生工作階段ID的唯一ID。 |

>[!NOTE]
>
>`__sid__`參數由雙下划線字元包圍。

資訊清單伺服器會維護個別用戶端或用戶端群組的工作階段，以確保不同用戶端的API互動順序保持不同。 客戶端在引導URL中發送到manifest伺服器的`__sid__`在其環境中應是唯一的。 資訊清單伺服器使用它來建構全域唯一ID，並傳回給用戶端。

其餘的查詢參數與不同的客戶端和情況有關。