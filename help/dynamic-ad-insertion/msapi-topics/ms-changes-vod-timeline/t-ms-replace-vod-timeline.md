---
description: 以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。
seo-description: 以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。
seo-title: 取代VOD時間軸
title: 取代VOD時間軸
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 取代VOD時間軸 {#replace-a-vod-timeline}

以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。

1. 以一般方式準備廣告插入請求。
1. 將查詢 `ptcueformat` 參數設為DPIScte35。
1. 視需要 `enableC3` 將查詢參數設為true或false。
1. 使用VOD時 `pttimeline` 間軸格式建立參數：
   1. 使用和指定每個內容區塊（章節） `duration = 0``number_of_lots = 1`。
   1. 照常指定每個廣告區塊，但設 `lots = 0` 定為移除分隔。 設 `duration = 0` 定為使用廣告插播的持續時間（來自M3U8檔案）。

## 範例：取代VOD時間軸

此範例假設VOD內容與 `Original.m3u8` 時間軸 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

下列資訊清單伺服器要求會 `Original.m3u8` 以30秒前段取代中的中斷，接著是兩個持續2分鐘的中斷。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

下列資訊清單伺服器要求會移除 `Original.m3u8` 中的中斷，並新增30秒前段和30秒後段。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
