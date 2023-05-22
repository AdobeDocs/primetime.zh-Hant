---
description: 所有廣告插入請求都使用相同的URL結構和相同的基本查詢參數。 附加查詢參數使清單伺服器能夠處理各種客戶機和情況。
title: 廣告插入請求
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# 廣告插入請求 {#requests-for-ad-insertion}

所有廣告插入請求都使用相同的URL結構和相同的基本查詢參數。 附加查詢參數使清單伺服器能夠處理各種客戶機和情況。

| 參數 | 說明 |
|--- |--- |
| 烏 | 資產ID是來自Adobe Primetime和決策元資料的ad_request_id的MD5哈希。 由Adobe技術客戶經理提供。 |
| z | 需要提供給Auditude的資產的區域ID。 由Adobe技術客戶經理提供。 |
| `__sid__` | 清單伺服器將用於生成會話ID的唯一ID。 |

>[!NOTE]
>
>的 `__sid__` 參數由雙下划線字元包圍。

清單伺服器維護單個客戶機或客戶機組的會話，以確保不同客戶機的API交互序列保持獨立。 的 `__sid__` 客戶機在引導URL中發送到清單伺服器的資訊在其環境中應是唯一的。 清單伺服器使用它構造全局唯一ID，並將其返回給客戶端。

其餘的查詢參數與不同的客戶機和情況有關。