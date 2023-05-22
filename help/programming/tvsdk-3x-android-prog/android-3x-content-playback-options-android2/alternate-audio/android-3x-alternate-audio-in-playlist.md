---
description: 視頻的播放清單可以指定用於主視頻內容的無限數量的備用音頻軌道。 例如，您可能希望向視頻內容添加不同的語言，或者允許用戶在播放內容時在其設備上的不同軌道之間切換。
title: 播放清單中的備用音頻軌道
exl-id: 3b892c8f-eb4f-4caf-b360-4781895a4022
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 播放清單中的備用音頻軌道 {#alternate-audio-tracks-in-the-playlist}

視頻的播放清單可以指定用於主視頻內容的無限數量的備用音頻軌道。 例如，您可能希望向視頻內容添加不同的語言，或者允許用戶在播放內容時在其設備上的不同軌道之間切換。

備用音頻軌道允許用戶在HTTP視頻流（即時/線性和VOD）的多語言軌道之間切換，並且您不必為每個音頻軌道修改、複製或重新打包視頻。 您可以為視頻資產在初始打包之前或之後提供多種語言跟蹤。

>[!IMPORTANT]
>
>要使備用音頻與主媒體的視頻軌道混合，備用軌道的時間戳必須與主軌道中音頻的時間戳相匹配。

主音軌被包括在音頻軌道集合中 `default` 的子菜單。 備用音頻流的元資料包括在 `#EXT-X-MEDIA` 標籤 `TYPE=AUDIO`。

例如，指定多個備用音頻流的M3U8清單可能如下所示：

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...
```
