---
description: 視訊的播放清單可為主要視訊內容指定不限數量的替代音軌。 例如，您可能會想要將不同的語言新增至視訊內容，或允許使用者在播放內容時，在其裝置上的不同曲目之間切換。
title: 播放清單中的替代音訊曲目
exl-id: 3b892c8f-eb4f-4caf-b360-4781895a4022
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 播放清單中的替代音訊曲目 {#alternate-audio-tracks-in-the-playlist}

視訊的播放清單可為主要視訊內容指定不限數量的替代音軌。 例如，您可能會想要將不同的語言新增至視訊內容，或允許使用者在播放內容時，在其裝置上的不同曲目之間切換。

替代音訊曲目可讓使用者在HTTP視訊串流的多個語言曲目之間切換（即時/線性和VOD），而且您不需要為每個音訊曲目修改、複製或重新封裝視訊。 您可以在視訊資產初始封裝之前或之後，為視訊資產提供多個語言追蹤。

>[!IMPORTANT]
>
>對於要與主要媒體的視訊曲目混合的替代音訊，替代曲目的時間戳記必須與主要曲目中音訊的時間戳記相符。

主要音軌包含在音軌集合中，並具有 `default` 標籤。 替代音訊串流的中繼資料會包含在播放清單的 `#EXT-X-MEDIA` 標籤與 `TYPE=AUDIO`.

例如，指定多個替代音訊資料流的M3U8資訊清單可能如下所示：

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
