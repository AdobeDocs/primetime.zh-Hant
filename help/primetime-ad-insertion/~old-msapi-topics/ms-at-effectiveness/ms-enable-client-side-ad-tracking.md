---
description: 您可以將pttrackingmode和pttrackingversion參數新增至您的BootstrapURL請求，以啟用用戶端廣告追蹤。
title: 啟用用戶端廣告追蹤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 2%

---


# 啟用用戶端廣告追蹤{#enable-client-side-ad-tracking}

您可以將`pttrackingmode`和`pttrackingversion`參數新增至您的BootstrapURL請求，以啟用用戶端廣告追蹤。

啟用用戶端廣告追蹤後，您也可以使用追蹤API URL擷取廣告追蹤中繼資料。 如需詳細資訊，請參閱[查詢參數](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)。

若要執行用戶端廣告追蹤，請使用追蹤API URL。

1. 新增下列查詢參數至資訊清單伺服器請求URL:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

例如：

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
