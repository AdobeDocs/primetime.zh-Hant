---
description: 來源清單中的forceflash旗標會強制URL的Flash後援。 對於此URL，您可以使用AdobeFlash Player來播放內容。
title: 使用媒體來源清單強制Flash回退
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# 使用媒體來源清單強制Flash回退{#forcing-the-flash-fallback-using-the-media-source-list}

來源清單中的forceflash旗標會強制URL的Flash後援。 對於此URL，您可以使用AdobeFlash Player來播放內容。

在媒體源清單（例如，在`sources.js`檔案中）中，可以將`forceflash`設定為`true`。 例如：

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```

