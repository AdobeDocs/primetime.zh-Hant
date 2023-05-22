---
description: 客戶端廣告插入請求通常在變型M3U8格式的播放清單中指定一個以上的比特率。 清單伺服器生成並返回新的變型M3U8檔案，該新變型M3U8檔案包含針對每個比特率的單獨M3U8鏈路。 它還生成一個唯一的組ID來將這些M3U8連接在一起。
title: 多比特率流
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 多比特率流 {#multiple-bit-rate-streams}

客戶端廣告插入請求通常在變型M3U8格式的播放清單中指定一個以上的比特率。 清單伺服器生成並返回新的變型M3U8檔案，該新變型M3U8檔案包含針對每個比特率的單獨M3U8鏈路。 它還生成一個唯一的組ID來將這些M3U8連接在一起。

清單伺服器使用客戶端的BootstrapURL請求中的資訊來檢索內容變體播放清單。 它生成一個新的變型播放清單，該播放清單包含到流級內容的清單伺服器連結。 客戶端使用它們構造和插入請求。 清單伺服器的流級內容連結具有以下格式：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 清單伺服器根據內容的播放清單類型設定此值：即時/線性(#EXT-X-PLAYLIST-TYPE:EVENT)或VOD(#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** Publisher針對BootstrapURL請求中提供的特定內容的唯一ID。

* **`rendition`** 清單伺服器基於內容流的BANDWIDTH值設定此值，並使用它將廣告的比特率與內容的比特率匹配。 除非具有最低比特率的廣告格式副本超過內容的比特率，否則廣告比特率不能超過內容的比特率。

* **`groupID`** 清單伺服器生成此值，並使用它來確保它始終如一地放置廣告，而不管客戶請求廣告的格式副本為什麼。

* **`base64-encoded url of the bit rate stream`** 清單伺服器URL安全base64對內容流的絕對URL進行編碼。 每個流都有其自己的URL。

* **`Query parameters`** 在BootstrapURL請求中提供的查詢參數。

