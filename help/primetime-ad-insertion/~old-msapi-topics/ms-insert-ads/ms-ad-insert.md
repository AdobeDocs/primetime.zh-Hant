---
description: 所有廣告插入請求都會使用相同的URL結構和相同的基本查詢引數。 其他查詢引數可讓資訊清單伺服器搭配各種使用者端和情況運作。
title: 廣告插入請求
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 廣告插入請求 {#requests-for-ad-insertion}

所有廣告插入請求都會使用相同的URL結構和相同的基本查詢引數。 其他查詢引數可讓資訊清單伺服器搭配各種使用者端和情況運作。

| 引數 | 說明 |
|--- |--- |
| u | 資產ID是Adobe Primetime ad decisioning中繼資料中ad_request_id的MD5雜湊。 由您的Adobe技術客戶經理提供。 |
| z | 需要提供給Auditude的資產區域ID。 由您的Adobe技術客戶經理提供。 |
| `__sid__` | 資訊清單伺服器用來產生工作階段ID的唯一ID。 |

>[!NOTE]
>
>此 `__sid__` 引數周圍有雙底線字元。

資訊清單伺服器會維護個別使用者端或使用者端群組的工作階段，以確保不同使用者端的API互動順序保持獨立。 此 `__sid__` 使用者端在啟動程式URL中傳送至資訊清單伺服器的行為，在其環境中應是唯一的。 資訊清單伺服器會使用它來建構全域唯一的ID，並傳回給使用者端。

其餘的查詢引數適用於不同的使用者端和情況。