---
description: 來源清單中的forceflash旗標會強制URL的Flash遞補。 對於此URL，您可以使用AdobeFlash Player來播放內容。
title: 使用媒體來源清單強制Flash遞補
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# 使用媒體來源清單強制Flash遞補{#forcing-the-flash-fallback-using-the-media-source-list}

來源清單中的forceflash旗標會強制URL的Flash遞補。 對於此URL，您可以使用AdobeFlash Player來播放內容。

在媒體來源清單中(例如 `sources.js` 檔案)，您可以設定 `forceflash` 至 `true`. 例如：

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
