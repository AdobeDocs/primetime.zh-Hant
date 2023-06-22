---
description: 使用選用的pttrackingmode、pttrackingversion和pttrackingposition查詢引數來取得URL，以將目前視訊的廣告追蹤資訊傳送至此。 回應會因追蹤版本以及視訊串流為即時或隨選(VOD)而異。
title: 播放器的API可與資訊清單伺服器互動
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 播放器的API可與資訊清單伺服器互動 {#api-for-players-to-interact-with-the-manifest-server}

使用選填的 `pttrackingmode`， `pttrackingversion`、和 `pttrackingposition` 查詢引數以取得要傳送目前視訊廣告追蹤資訊的URL。 回應會因追蹤版本以及視訊串流為即時或隨選(VOD)而異。

## 查詢引數 {#query-parameters}

**pttrackingmode**

範例： `pttrackingmode=simple`
指定simple會告訴資訊清單伺服器您要追蹤資訊。
在您要求追蹤資訊之前，在要求擷取M3U8時指定它。若您未指定，資訊清單伺服器會傳回#EXT-X-MARKER標籤中的追蹤資訊。
或者，如果您指定簡單以外的有效值，則會叫用伺服器端追蹤。

**pttrackingversion**

範例： `pttrackingversion=v2`
此引數會告訴資訊清單伺服器使用哪種格式來傳回追蹤資訊(請參閱 [檔案格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。
在要求擷取M3U8的請求中指定它，然後再要求追蹤資訊。若未指定它或指定無效值，資訊清單伺服器會使用v1。

**pttrackingposition**

範例： `pttrackingposition`
此引數會告訴資訊清單伺服器傳回視訊的追蹤資訊，作為M3U8檔案中的JSON或VMAP物件。資訊清單伺服器會忽略指定的值，並傳送其對於該工作階段擁有的所有追蹤資訊。 如果未傳遞任何值，資訊清單伺服器會傳回請求的M3U8檔案。
