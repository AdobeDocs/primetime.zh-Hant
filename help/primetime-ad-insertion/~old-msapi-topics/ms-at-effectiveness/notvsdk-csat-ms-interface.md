---
description: 使用可選的pttrackingmode、pttrackingversion和pttrackingposition查詢參數可獲取要向其發送有關當前視頻的廣告跟蹤資訊的URL。 響應隨跟蹤版本和視頻流是即時還是按需(VOD)而變化。
title: 用於玩家與清單伺服器交互的API
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 用於玩家與清單伺服器交互的API {#api-for-players-to-interact-with-the-manifest-server}

使用可選 `pttrackingmode`。 `pttrackingversion`, `pttrackingposition` 查詢參數以獲取要向其發送有關當前視頻的廣告跟蹤資訊的URL。 響應隨跟蹤版本和視頻流是即時還是按需(VOD)而變化。

## 查詢參數 {#query-parameters}

**跟蹤模式**

示例： `pttrackingmode=simple`
指定simple會告訴清單伺服器您想要跟蹤資訊。
在請求跟蹤資訊之前，請在請求獲取M3U8時指定它。如果未指定它，清單伺服器將返回#EXT-X-MARKER標籤中的跟蹤資訊。
或者，如果指定除簡單跟蹤之外的有效值，則會調用伺服器端跟蹤。

**pttrackingversion**

示例： `pttrackingversion=v2`
此參數將告訴清單伺服器返回跟蹤資訊時要使用的格式(請參閱 [檔案格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md))。
在請求跟蹤資訊之前，請在請求獲取M3U8時指定它。如果未指定它或指定了無效值，清單伺服器將使用v1。

**跟蹤位置**

示例： `pttrackingposition`
此參數指示清單伺服器以M3U8檔案中的JSON或VMAP對象形式返回視頻的跟蹤資訊。清單伺服器忽略指定值併發送它為該會話擁有的所有跟蹤資訊。 如果未傳遞值，則清單伺服器返回請求的M3U8檔案。
