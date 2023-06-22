---
description: 除了基本查詢引數之外，選用的查詢引數可讓資訊清單伺服器搭配不同的使用者端和情況運作。
title: 依使用者端和情境區分的選用查詢引數
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# 依使用者端和情境區分的選用查詢引數 {#optional-query-parameters-by-client-and-situation}

除了基本查詢引數之外，選用的查詢引數可讓資訊清單伺服器搭配不同的使用者端和情況運作。

## 使用Akamai Ad Scaler插入廣告 {#section_120FEC75C34D4F4587B77D842166D68A}

在Akamai內容傳遞網路(CDN)上，Akamai Edge伺服器會作為使用者端與資訊清單伺服器之間的中介運作。 如果您也使用「廣告縮放器」，則 `ptassetid` 和 `live` 查詢引數會向Akamai Edge提供必要資訊。

此 `ptassetid` parameter是發佈者資產的ID。 Akamai會使用此（而不是您當作請求URL的一部分提供的base64編碼URL）來識別要提供給資訊清單伺服器以進行廣告插入的播放清單。

此 `live` 引數會區分即時內容和隨選影片(VOD)。 資訊清單伺服器需要此資訊，才能支援其簡化的Akamai介面。

以下是顯示與Akamai相關之引數的範例URL：

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## 從Xbox上的TVSDK插入廣告 {#section_5DB405F4647240A0B83E72DE35D5EC80}

以Xbox上的Primetime TVSDK為基礎的播放器，不需要提供基本引數以外的其他查詢引數。

## 使用Safari在iOS上從TVSDK插入廣告 {#section_250E493A125E4F82940D19C7DA2AAB2E}

使用Safari瀏覽器且以iOS上的Primetime TVSDK為基礎的播放器必須指定 `ptplayer` 和 `live` 基本查詢引數以外的引數。

資訊清單伺服器會辨識 `ptplayer` 值 `ios-mobileweb` 並從其傳回的廣告拼接資訊清單中移除前段。

此 `live` parameter告訴資訊清單伺服器是傳回即時內容還是VOD內容。

以下範例URL顯示與使用Safari的iOS相關的引數：

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自訂廣告提示格式的廣告插入 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe提供不直接在Primetime套件中支援的廣告提示格式名稱。 若要使用這類格式，請提供其Adobe提供的名稱作為 `ptcueformat` 引數。

指定自訂廣告提示格式的URL範例如下：

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用廣告提示為VOD建立FreeWheel時間軸的廣告插入 {#section_E0D830F5EEE24639819B975B90F6999F}

對於包含要剖析並包含在FreeWheel廣告請求中的廣告提示的VOD內容，請將 `ptcueformat` 引數至 `DPIsimple`.

以下是URL範例，其指定使用VOD的FreeWheel時間軸：

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用VOD的自訂時間表進行廣告插入 {#section_F398F7659164463FA886A4CC787C7B5A}

若要要求資訊清單伺服器根據您提供的時間軸將廣告插入VOD內容，請設定 `pttimeline` 字串的引數，指定時間軸。 另請參閱 [VOD時間表格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

以下是VOD使用自訂時間軸的範例URL：

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

其指定一分鐘的初始中斷，最多包含兩個廣告，接著是兩分鐘的內容區段，然後是最多包含兩個廣告的30秒中斷，接著是五分鐘的內容區段。

VOD內容的自訂內容時間軸的廣告拼接行為如下：

* 廣告會出現在廣告伺服器指定的廣告放置時間後最接近的插播邊界處。

* 區段的長度至少為兩秒。

## 授權TS區段 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe僅對Akamai CDN支援此功能。 HTTP即時資料流(HLS)使用資料流層級M3U8播放清單來傳送傳輸資料流(TS)區段。 以變體M3U8播放清單的形式提供多個串流層級播放清單給使用者端。 使用者端從變體清單中挑選一個播放清單串流，然後逐一下載該串流層級播放清單中的TS區段。 在正常操作中，請求的內容可能需要Cookie授權，資訊清單伺服器會在背景以不可見的方式處理此授權。 它會從原始內容中擷取Cookie，並將適當的權杖附加至URL，以用於請求所選的播放清單資料流。

當BootstrapURL查詢引數包括 `pttoken=true`，發佈者會要求在請求每個TS區段中使用Cookie，而不是只要求對整個資料流使用一次。 資訊清單伺服器會將此Cookie作為查詢引數附加至其傳回的串流播放清單中的每個TS區段URL。
