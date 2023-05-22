---
description: 適合視頻點播內容之一播放的廣告時間線可能不適合後續播放。 您可以替換VOD時間線，而不更改內容。
title: 對VOD的更改
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# 對VOD的更改 {#changes-to-vod}

適合視頻點播內容之一播放的廣告時間線可能不適合後續播放。 您可以替換VOD時間線，而不更改內容。

您可能希望替換VOD時間線的情況包括：

* 替換本地廣告，但在C3窗口中保留全國廣告。
* 在C3窗口關閉後更換燒入廣告。
* 動態地將舊的C3廣告替換為持續時間更長的較新廣告。
* 插入更少的廣告或根本沒有廣告。

您可以通過提交新的廣告插入請求來替換廣告時間線，該請求使用原始M3U8檔案和 `pttimeline` 查詢參數。