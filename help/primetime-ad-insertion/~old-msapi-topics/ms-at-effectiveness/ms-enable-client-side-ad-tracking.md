---
description: 通過向BootstrapURL請求添加pttrackingmode和pttrackingversion參數，可以啟用客戶端和跟蹤。
title: 啟用客戶端廣告跟蹤
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 啟用客戶端廣告跟蹤 {#enable-client-side-ad-tracking}

通過添加 `pttrackingmode` 和 `pttrackingversion` BootstrapURL請求的參數。

啟用客戶端和跟蹤後，您還可以使用跟蹤API URL檢索和跟蹤元資料。 有關詳細資訊，請參閱 [查詢參數](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)。

要執行客戶端和跟蹤，請使用跟蹤API URL。

1. 將以下查詢參數添加到清單伺服器請求URL:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

例如：

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
