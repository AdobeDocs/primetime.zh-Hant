---
description: 適合一個VOD內容播放的廣告時間表可能不適合後續播放。 您可以取代VOD時間軸而不變更內容。
title: VOD的變更
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# VOD的變更 {#changes-to-vod}

適合一個VOD內容播放的廣告時間表可能不適合後續播放。 您可以取代VOD時間軸而不變更內容。

您可能想要取代VOD時間軸的情況包括：

* 取代當地廣告，但在C3視窗中保留國內廣告。
* 在C3視窗關閉後取代燒錄廣告。
* 以持續時間較長的較新廣告動態取代舊的C3廣告。
* 插入較少廣告或完全不插入廣告。

您可以透過提交新的廣告插入請求來取代廣告時間表，方法是使用原始M3U8檔案和的不同值 `pttimeline` 查詢引數。