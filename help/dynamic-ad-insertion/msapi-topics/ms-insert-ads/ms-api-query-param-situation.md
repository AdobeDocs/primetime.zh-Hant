---
description: 除了基本查詢參數，可選查詢參數還可讓資訊清單伺服器搭配不同的用戶端和情況運作。
seo-description: 除了基本查詢參數，可選查詢參數還可讓資訊清單伺服器搭配不同的用戶端和情況運作。
seo-title: 依用戶端和情況選擇的查詢參數
title: 依用戶端和情況選擇的查詢參數
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# 按客戶端和情況列出的可選查詢參數{#optional-query-parameters-by-client-and-situation}

除了基本查詢參數，可選查詢參數還可讓資訊清單伺服器搭配不同的用戶端和情況運作。

## 使用Akamai廣告縮放器{#section_120FEC75C34D4F4587B77D842166D68A}插入廣告

在Akamai內容傳送網路(CDN)上，Akamai Edge伺服器是用戶端與資訊清單伺服器之間的中介。 如果您也使用廣告縮放器，`ptassetid`和`live`查詢參數會為Akamai Edge提供必要資訊。

`ptassetid`參數是發行者的資產ID。 Akamai會使用這個，而非您在請求URL中提供的base64編碼URL，來識別要提供給資訊清單伺服器以進行廣告插入的播放清單。

`live`參數可區分即時內容與隨選視訊(VOD)。 資訊清單伺服器需要這些資訊，以支援其與Akamai的簡化介面。

以下是顯示與Akamai相關參數的範例URL:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## 從Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}上的TVSDK插入廣告

以Primetime TVSDK為基礎的Xbox播放器，不需要提供其他基本查詢參數。

## 在iOS上使用Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}從TVSDK插入廣告

使用Safari瀏覽器的iOS上以Primetime TVSDK為基礎的播放器，除了基本查詢參數外，還必須指定`ptplayer`和`live`參數。

資訊清單伺服器會辨識`ptplayer`值`ios-mobileweb`，並從它傳回的廣告銜接資訊清單中消除預先統計。

`live`參數會告訴資訊清單伺服器要傳回即時或VOD內容。

以下是範例URL，其中顯示與iOS與Safari相關的參數：

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自訂廣告提示格式{#section_82AF880AAABE4BD4B593D906434D4D89}的廣告插入

Adobe提供其不直接在Primetime套件中支援的廣告提示格式名稱。 若要使用此格式，請提供其Adobe提供的名稱作為`ptcueformat`參數的值。

以下是指定自訂廣告提示格式的範例URL:

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用廣告提示建立VOD {#section_E0D830F5EEE24639819B975B90F6999F}的FreeWheel時間軸的廣告插入

對於包含要解析並包含在FreeWheel廣告請求中的廣告提示的VOD內容，請將`ptcueformat`參數的值設為`DPIsimple`。

以下是指定使用FreeWheel時間軸進行VOD的範例URL:

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用VOD {#section_F398F7659164463FA886A4CC787C7B5A}的自訂時間軸來插入廣告

若要要求資訊清單伺服器根據您提供的時間軸將廣告插入VOD內容，請將`pttimeline`參數的值設定為指定時間軸的字串。 請參閱[VOD時間軸格式](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

以下是使用自訂時間軸的VOD範例URL:

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

它指定最多包含兩個廣告的1分鐘初始分隔，接著是2分鐘內容區段，接著是30秒分隔，最多包含兩個廣告，接著是5分鐘內容區段。

VOD內容的自訂內容時間軸的廣告拼接如下所示：

* 廣告會出現在廣告伺服器指定的廣告放置時間之後最接近的中斷邊界。
* 區段至少有兩秒長。

## 授權TS段{#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe僅支援Akamai CDN的這項功能。 HTTP即時串流(HLS)使用串流層級的M3U8播放清單來傳送傳輸串流(TS)區段。 在變型M3U8播放清單中，將多個串流層級播放清單提供給用戶端。 用戶端從變型清單中選擇一個播放清單串流，然後逐一下載該串流層級播放清單中的TS區段。 在正常操作中，所請求的內容可能需要Cookie授權，資訊清單伺服器會在背景以不可見方式處理。 它會從原始內容擷取Cookie，並附加適當的Token至URL，以用於請求選取的播放清單串流。

當引導URL查詢參數包含`pttoken=true`時，發佈者會要求使用Cookie來請求每個TS區段，而不是只請求整個串流一次。 資訊清單伺服器會將此Cookie附加為查詢參數，以連結至其傳回之串流播放清單中的每個TS區段URL。
