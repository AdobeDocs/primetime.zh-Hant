---
description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，資訊清單伺服器會傳回包含Master-M3U8的JSON格式檔案，這是使用者端用來要求描述內容的M3U8檔案的URL。
title: 請求變體資訊清單播放清單的URL的JSON格式
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 請求變體資訊清單播放清單的URL的JSON格式 {#json-format-for-url-for-requesting-variant-manifest-playlist}

若 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb`，資訊清單伺服器會傳回包含Master-M3U8的JSON格式檔案，這是使用者端用來要求M3U8檔案（說明內容）的URL。

這是包含的JSON檔案格式 `Master-M3U8` URL。

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
