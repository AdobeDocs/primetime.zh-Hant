---
description: 您可以將pttrackingmode和pttrackingversion引數新增至BootstrapURL請求，以啟用使用者端廣告追蹤。
title: 啟用使用者端廣告追蹤
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 啟用使用者端廣告追蹤 {#enable-client-side-ad-tracking}

您可以透過新增以下專案來啟用使用者端廣告追蹤： `pttrackingmode` 和 `pttrackingversion` BootstrapURL要求的引數。

啟用使用者端廣告追蹤後，您也可以使用追蹤API URL擷取廣告追蹤中繼資料。 如需詳細資訊，請參閱 [查詢引數](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

若要執行使用者端廣告追蹤，請使用追蹤API URL。

1. 將下列查詢引數新增至資訊清單伺服器要求URL：

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

例如：

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
