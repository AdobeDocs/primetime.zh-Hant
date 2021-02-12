---
description: 用戶端廣告插入要求通常會在變數的M3U8格式播放清單中指定多個位元速率。 資訊清單伺服器會產生並傳回新的變型M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，將這些M3U8系結在一起。
seo-description: 用戶端廣告插入要求通常會在變數的M3U8格式播放清單中指定多個位元速率。 資訊清單伺服器會產生並傳回新的變型M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，將這些M3U8系結在一起。
seo-title: 多位元速率串流
title: 多位元速率串流
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# 多位速率串流{#multiple-bit-rate-streams}

用戶端廣告插入要求通常會在變數的M3U8格式播放清單中指定多個位元速率。 資訊清單伺服器會產生並傳回新的變型M3U8檔案，其中包含每個位元速率的個別M3U8連結。 它也會產生唯一的群組ID，將這些M3U8系結在一起。

資訊清單伺服器使用用戶端的引導URL請求中的資訊來擷取內容變體播放清單。 它產生包含串流層級內容之資訊清單伺服器連結的新變型播放清單。 用戶端會使用這些項目來建構廣告插入請求。 資訊清單伺服器的串流層級內容連結具有下列格式：

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** 資訊清單伺服器會根據內容的播放清單類型來設定此值：即時／線性(#EXT-X-PLAYLIST-TYPE:EVENT)或VOD(#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** 發佈者針對引導URL請求中提供之特定內容的唯一ID。

* **`rendition`** 資訊清單伺服器根據內容串流的BANDWIDTH值來設定此資訊，並使用它來比對廣告的位元速率與內容的位元速率。廣告位元速率不得超過內容的位元速率，除非具有最低位元速率的廣告轉譯如此。

* **`groupID`** 資訊清單伺服器會產生此值，並使用它來確保廣告放置一致，不論用戶端要求廣告的位元速率轉譯為何。

* **`base64-encoded url of the bit rate stream`** 資訊清單伺服器URL安全base64會對內容串流的絕對URL進行編碼。每個串流都有其專屬的URL。

* **`Query parameters`** 引導URL請求中提供的查詢參數。

