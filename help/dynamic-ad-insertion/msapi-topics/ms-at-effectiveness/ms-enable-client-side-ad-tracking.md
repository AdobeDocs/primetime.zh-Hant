---
description: 您可以將pttrackingmode和pttrackingversion參數新增至您的引導URL請求，以啟用用戶端廣告追蹤。
seo-description: 您可以將pttrackingmode和pttrackingversion參數新增至您的引導URL請求，以啟用用戶端廣告追蹤。
seo-title: 啟用用戶端廣告追蹤
title: 啟用用戶端廣告追蹤
uuid: 0a825756-1d9a-43c5-bc22-9b366f39fdbb
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 啟用用戶端廣告追蹤 {#enable-client-side-ad-tracking}

您可以新增和參數至您的引導URL請求， `pttrackingmode` 以啟 `pttrackingversion` 用用戶端廣告追蹤。

啟用用戶端廣告追蹤後，您也可以使用追蹤API URL擷取廣告追蹤中繼資料。 如需詳細資訊，請參 [閱查詢參數](../../msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)。

若要執行用戶端廣告追蹤，請使用追蹤API URL。

1. 新增下列查詢參數至資訊清單伺服器請求URL:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

例如：

```
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
