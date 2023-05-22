---
description: 除了基本查詢參數之外，可選查詢參數還使清單伺服器能夠處理不同的客戶機和情況。
title: 按客戶端和情況列出的可選查詢參數
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# 按客戶端和情況列出的可選查詢參數 {#optional-query-parameters-by-client-and-situation}

除了基本查詢參數之外，可選查詢參數還使清單伺服器能夠處理不同的客戶機和情況。

## Akamai廣告插入 {#section_120FEC75C34D4F4587B77D842166D68A}

在Akamai內容傳遞網路(CDN)上，Akamai邊緣伺服器充當客戶機和清單伺服器之間的中介。 如果您還使用Ad Scaler, `ptassetid` 和 `live` 查詢參數向Akamai邊緣提供所需資訊。

的 `ptassetid` 參數是其資產的發佈者ID。 Akamai使用此（而不是作為請求URL一部分提供的base64編碼URL）來標識要提供給清單伺服器以進行廣告插入的播放清單。

的 `live` 參數區分即時內容和視頻點播(VOD)。 清單伺服器需要此資訊來支援其與Akamai的簡化介面。

下面是一個示例URL，它顯示與Akamai相關的參數：

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## 從Xbox上的TVSDK插入廣告 {#section_5DB405F4647240A0B83E72DE35D5EC80}

基於Xbox上的Bogki時TVSDK的播放器無需提供基本的查詢參數之外的其他查詢參數。

## TVSDK在iOS上與Safari一起插入廣告 {#section_250E493A125E4F82940D19C7DA2AAB2E}

使用Safari瀏覽器基於iOS黃金時段TVSDK的播放器必須指定 `ptplayer` 和 `live` 除基本查詢參數外，還有參數。

清單伺服器識別 `ptplayer` 值 `ios-mobileweb` 並從它返回的廣告縫合清單中消除預滾。

的 `live` 參數指示清單伺服器是返回即時內容還是VOD內容。

下面是一個示例URL，它顯示與Safari有關的iOS參數：

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## 使用自定義廣告提示格式的廣告插入 {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe為Mogife包中不直接支援的廣告提示格式提供名稱。 要使用此格式，請提供其Adobe提供的名稱作為 `ptcueformat` 的下界。

下面是一個指定自定義提示格式的示例URL:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## 使用廣告提示建立用於VOD的FreeWheel時間線的廣告插入 {#section_E0D830F5EEE24639819B975B90F6999F}

對於包含要被解析並包含在FreeWheel廣告請求中的廣告提示的VOD內容，設定 `ptcueformat` 參數 `DPIsimple`。

下面是一個示例URL，它指定對VOD使用FreeWheel時間線：

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## 使用用於視頻點播的定製時間線的廣告插入 {#section_F398F7659164463FA886A4CC787C7B5A}

要請求清單伺服器根據您提供的時間表將廣告插入VOD內容，請設定 `pttimeline` 指定時間軸的字串的參數。 請參閱 [VOD時間線格式](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)。

下面是一個示例URL，它使用自定義時間表進行VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

它指定了一分鐘的初始休息，最多包含兩個廣告，然後是兩分鐘的內容段，然後是最多包含兩個廣告的30秒休息，最後是五分鐘的內容段。

VOD內容的自定義內容時間線的廣告縫合如下所示：

* 廣告出現在廣告伺服器指定的廣告投放時間之後最近的中斷邊界處。

* 段長度至少為2秒。

## 授權TS段 {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe僅支援Akamai CDN的此功能。 HTTP即時流(HLS)使用流級M3U8播放清單來傳送傳輸流(TS)段。 在變型M3U8播放清單中向客戶機提供多個流級播放清單。 客戶端從變型清單中選擇一個播放清單流，然後逐個下載該流級播放清單中的TS段。 在正常操作中，請求的內容可能需要Cookie授權，清單伺服器在後台以不可見方式處理該授權。 它從原始內容中提取cookie，並將適當的令牌附加到URL，以用於請求所選播放清單流。

當BootstrapURL查詢參數包括 `pttoken=true`，發佈者要求在請求每個TS段時使用cookie ，而不是僅對整個流使用一次。 清單伺服器將此cookie作為查詢參數附加到它發送回的流播放清單中的每個TS段URL。
