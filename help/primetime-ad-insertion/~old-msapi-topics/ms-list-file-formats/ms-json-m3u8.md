---
description: 如果pttrackingmode=simple或ptplayer=ios-mobileweb，清單伺服器將發回包含Master-M3U8的JSON格式檔案，該URL用於客戶端請求描述內容的M3U8檔案。
title: 用於請求變型清單播放清單的URL的JSON格式
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 用於請求變型清單播放清單的URL的JSON格式 {#json-format-for-url-for-requesting-variant-manifest-playlist}

如果 `pttrackingmode=simple` 或 `ptplayer=ios-mobileweb`，清單伺服器將返回包含Master-M3U8的JSON格式檔案，該URL供客戶端請求描述內容的M3U8檔案。

這是包含JSON檔案的格式 `Master-M3U8` URL。

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
