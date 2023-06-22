---
description: 使用適當設定的時間表查詢引數，將新的廣告插入請求傳送至資訊清單伺服器，以取代VOD時間表。
title: 取代VOD時間表
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 取代VOD時間表 {#replace-a-vod-timeline}

使用適當設定的時間表查詢引數，將新的廣告插入請求傳送至資訊清單伺服器，以取代VOD時間表。

1. 以一般方式準備廣告插入請求。
1. 設定 `ptcueformat` dpiscte35的查詢引數。
1. 設定 `enableC3` 將查詢引數設為true或false （視情況而定）。
1. 建立 `pttimeline` 使用VOD時間軸格式的引數：
   1. 指定每個內容區塊（章節），使用 `duration = 0` 和 `number_of_lots = 1`.
   1. 照常指定每個廣告區塊，但設定 `lots = 0` 以移除破斷。 設定 `duration = 0` 以使用廣告插播的持續時間（來自M3U8檔案）。

## 範例：取代VOD時間表

此範例假設VOD內容位於 `Original.m3u8` 時間軸為 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

以下資訊清單伺服器請求會取代中的中斷 `Original.m3u8` 前置時間為30秒，接著是兩個工期中斷，每次中斷兩分鐘。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下資訊清單伺服器要求移除中的中斷點 `Original.m3u8` 和會新增30秒的前段和30秒的後段影片。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
