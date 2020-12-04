---
description: 來源清單中的forceflash旗標會強制Flash回退URL。 對於此URL，您可以使用Adobe Flash Player播放內容。
seo-description: 來源清單中的forceflash旗標會強制Flash回退URL。 對於此URL，您可以使用Adobe Flash Player播放內容。
seo-title: 使用媒體來源清單強制Flash備援
title: 使用媒體來源清單強制Flash備援
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 1%

---


# 使用媒體來源清單強制Flash備援{#forcing-the-flash-fallback-using-the-media-source-list}

來源清單中的forceflash旗標會強制Flash回退URL。 對於此URL，您可以使用Adobe Flash Player播放內容。

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

