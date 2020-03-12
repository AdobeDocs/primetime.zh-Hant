---
description: 使用選用的pttrackingmode、pttrackingversion和pttrackingposition查詢參數，以取得要傳送目前視訊廣告追蹤資訊的URL。 回應會隨追蹤版本以及視訊串流是即時或隨選(VOD)而異。
seo-description: 使用選用的pttrackingmode、pttrackingversion和pttrackingposition查詢參數，以取得要傳送目前視訊廣告追蹤資訊的URL。 回應會隨追蹤版本以及視訊串流是即時或隨選(VOD)而異。
seo-title: 播放器與資訊清單伺服器互動的API
title: 播放器與資訊清單伺服器互動的API
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# 播放器與資訊清單伺服器互動的API {#api-for-players-to-interact-with-the-manifest-server}

使用選 `pttrackingmode`用、 `pttrackingversion`和查 `pttrackingposition` 詢參數，以取得要傳送目前視訊廣告追蹤資訊的URL。 回應會隨追蹤版本以及視訊串流是即時或隨選(VOD)而異。

## 查詢參數 {#query-parameters}

|**pttrackingmode**|範例：pttrackingmode=simple指定simple會告訴manifest伺服器您想要追蹤資訊。
請在要求追蹤資訊之前，先在要求時指定擷取M3U8。當您未指定資訊時，資訊清單伺服器會傳回#EXT-X-MARKER標籤中的追蹤資訊。
或者，如果您指定除了簡單以外的有效值，則會呼叫伺服器端追蹤。

|**pttrackingversion**|範例：pttrackingversion=v2此參數會告訴資訊清單伺服器要使用何種格式來傳回追蹤資訊(請參 [閱檔案格式](../../msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。
在要求追蹤資訊之前，請在要求時指定它以擷取M3U8。當您未指定它或指定無效值時，資訊清單伺服器會使用v1。

|**pttrackingposition**|範例：pttrackingposition此參數會告訴manifest伺服器，將視訊的追蹤資訊傳回為M3U8檔案中的JSON或VMAP物件。manifest伺服器會忽略指定值，並傳送它為該作業的所有追蹤資訊。 如果未傳遞值，manifest伺服器會傳回要求的M3U8檔案。