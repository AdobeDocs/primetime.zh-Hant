---
description: 一個廣告可能有多個創意，其中一個被選中播放。
title: 有效的MIME類型
exl-id: 878cae20-2a94-4795-8908-be7daffefb41
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 有效的MIME類型{#valid-mime-types}

一個廣告可能有多個創意，其中一個被選中播放。

使用MIME類型，可以指定用戶可以優先選擇哪些創作類型。 用戶指定的MIME類型和瀏覽器TVSDK支援的MIME類型用於確定將按優先順序排列哪些創作。

要在瀏覽器TVSDK中設定有效的MIME類型：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

何處 `mimeTypes` 是字串的陣列，每個字串都表示mime類型。

如果為廣告返回多個媒體檔案，則選擇取決於媒體檔案在 `validMimeTypes` 陣列。 具有較低索引的MIME類型比具有較高索引的MIME類型更優先。
