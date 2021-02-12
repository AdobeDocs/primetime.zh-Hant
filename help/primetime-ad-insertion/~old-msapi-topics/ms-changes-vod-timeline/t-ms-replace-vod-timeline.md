---
description: 以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。
seo-description: 以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。
seo-title: 取代VOD時間軸
title: 取代VOD時間軸
uuid: 17a6daa3-5ee5-48fb-8981-0d183aed0fe4
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 取代VOD時間軸{#replace-a-vod-timeline}

以適當設定的pttimeline查詢參數傳送新廣告插入請求至資訊清單伺服器，以取代VOD時間軸。

1. 以一般方式準備廣告插入請求。
1. 將`ptcueformat`查詢參數設為DPIScte35。
1. 視情況將`enableC3`查詢參數設為true或false。
1. 使用VOD時間軸格式建立`pttimeline`參數：
   1. 使用`duration = 0`和`number_of_lots = 1`指定每個內容區塊（章節）。
   1. 照常指定每個廣告區塊，但設定`lots = 0`以移除中斷。 設定`duration = 0`以使用廣告插播的持續時間（來自M3U8檔案）。

## 範例：取代VOD時間軸

此範例假設VOD內容位於`Original.m3u8`且時間軸為`C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

下列資訊清單伺服器要求會以30秒前段取代`Original.m3u8`中的中斷，接著兩次中斷，每次兩分鐘。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

下列資訊清單伺服器要求會移除`Original.m3u8`中的中斷，並新增30秒前段和30秒後段。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
