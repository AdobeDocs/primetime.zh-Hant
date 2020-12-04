---
description: 一個廣告可能有多個創意素材，其中一個是選取要播放的。
seo-description: 一個廣告可能有多個創意素材，其中一個是選取要播放的。
seo-title: 有效的MIME類型
title: 有效的MIME類型
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# 有效的mime類型{#valid-mime-types}

一個廣告可能有多個創意素材，其中一個是選取要播放的。

使用MIME類型，您可以指定使用者可以排定優先順序的創意類型。 使用者指定的MIME類型和瀏覽器TVSDK支援的MIME類型，會用來決定將哪些創意設定為優先順序。

若要在瀏覽器TVSDK中設定有效的MIME類型：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

其中`mimeTypes`是字串的陣列，而每個字串代表MIME類型。

如果廣告傳回多個媒體檔案，選擇會視媒體檔案在`validMimeTypes`陣列中的顯示順序而定。 具有較低索引的MIME類型比具有較高索引的MIME類型更優先。
