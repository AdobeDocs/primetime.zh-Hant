---
description: 通過用適當設定的時間線查詢參數向清單伺服器發送新的廣告插入請求來替換VOD時間線。
title: 替換VOD時間線
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 替換VOD時間線 {#replace-a-vod-timeline}

通過用適當設定的時間線查詢參數向清單伺服器發送新的廣告插入請求來替換VOD時間線。

1. 按常規方式準備廣告插入請求。
1. 設定 `ptcueformat` 查詢參數到DPIScte35。
1. 設定 `enableC3` 查詢參數為true或false（如適用）。
1. 建立 `pttimeline` 使用VOD時間線格式的參數：
   1. 指定每個內容塊（章） `duration = 0` 和 `number_of_lots = 1`。
   1. 按常規指定每個廣告塊，但設定 `lots = 0` 刪除中斷。 設定 `duration = 0` 使用廣告分段的持續時間（從M3U8檔案）。

## 示例：替換VOD時間線

此示例假定VOD內容在 `Original.m3u8` 和 `C,120,1;B,60,2,m;C,120,1;B,60,2,m;C,120,1;`

以下清單伺服器請求替換中的中斷 `Original.m3u8` 先進行30秒的預卷，然後再進行兩次間歇，每次兩分鐘。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,120,4,m;C,0,1;B,120,4,m;C,0,1;
```

以下清單伺服器請求將刪除中的中斷 `Original.m3u8` 加30秒前滾和30秒後滾。

```
https://manifest.auditude.com/auditude/variant/pubAsset/Original.m3u8?. . .&enableC3=false 
&pttimeline=B,30,2,p;C,0,1;B,0,0,m;C,0,1;B,0,0,m;C,0,1;B,30,2,t;
```
