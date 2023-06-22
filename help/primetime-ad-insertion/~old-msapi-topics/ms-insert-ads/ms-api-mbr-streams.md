---
description: 廣告插入的使用者端請求通常會在變體M3U8格式的播放清單中指定超過一個位元速率。 資訊清單伺服器會產生並傳回新的變體M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，以將這些M3U8繫結在一起。
title: 多位元速率資料流
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 多位元速率資料流 {#multiple-bit-rate-streams}

廣告插入的使用者端請求通常會在變體M3U8格式的播放清單中指定超過一個位元速率。 資訊清單伺服器會產生並傳回新的變體M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，以將這些M3U8繫結在一起。

資訊清單伺服器會使用使用者端BootstrapURL請求中的資訊來擷取內容變體播放清單。 它會產生包含資料流層級內容之資訊清單伺服器連結的新變體播放清單。 使用者端會使用這些來建構廣告插入請求。 資訊清單伺服器的串流層級內容連結格式如下：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 資訊清單伺服器會根據內容的播放清單型別設定此值：即時/線性(#EXT-X-PLAYLIST-TYPE：EVENT)或VOD (#EXT-X-PLAYLIST-TYPE：VOD)

* **`publisherAssetID`** Publisher在BootstrapURL要求中提供之特定內容的唯一ID。

* **`rendition`** 資訊清單伺服器會根據內容資料流的BANDWIDTH值設定此值，並使用它來比對廣告的位元速率與內容的位元速率。 廣告位元速率不能超過內容的位元速率，除非具有最低位元速率的廣告轉譯超過此速率。

* **`groupID`** 資訊清單伺服器會產生此值，並使用它來確保無論使用者端要求廣告的位元速率轉譯，都能一致地放置廣告。

* **`base64-encoded url of the bit rate stream`** 資訊清單伺服器URL安全的base64會編碼內容資料流的絕對URL。 每個資料流都有自己的URL。

* **`Query parameters`** BootstrapURL要求中提供的查詢引數。

