---
description: 一個廣告可能有多項創意，其中一項已選取播放。
title: 有效的MIME型別
exl-id: 878cae20-2a94-4795-8908-be7daffefb41
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 有效的MIME型別{#valid-mime-types}

一個廣告可能有多項創意，其中一項已選取播放。

對於MIME型別，您可以指定使用者可優先處理哪些創意型別。 使用者指定的MIME型別以及瀏覽器TVSDK支援的MIME型別，可用來判斷將優先處理哪些創意。

若要在瀏覽器TVSDK中設定有效的MIME型別：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

位置 `mimeTypes` 是一個字串陣列，而每個字串都代表mime型別。

如果針對廣告傳回多個媒體檔案，則選取範圍取決於媒體檔案出現的順序 `validMimeTypes` 陣列。 索引較低的MIME型別會比索引較高的型別獲得優先權。
