---
description: 視頻的播放清單可以為主視頻內容指定不限數量的替代音軌。 例如，您可能想要在視訊內容中加入不同的語言，或允許使用者在播放內容時在裝置上切換不同的音軌。
title: 播放清單中的替代音軌
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 播放清單中的替代音軌{#alternate-audio-tracks-in-the-playlist}

視頻的播放清單可以為主視頻內容指定不限數量的替代音軌。 例如，您可能想要在視訊內容中加入不同的語言，或允許使用者在播放內容時在裝置上切換不同的音軌。

替代音軌或延遲系結的音訊可讓使用者在HTTP視訊串流（即時／線性和VOD）的多種語言音軌之間切換，而您不需要針對每個音軌修改、複製或重新封裝視訊。 您可以在資產的初始封裝之前或之後，為視訊資產提供多種語言追蹤。

>[!TIP]
>
>若要將替代音訊與主媒體的視訊軌道混合，則替代音軌的時間戳記必須與主音軌中音訊的時間戳記相符。

主音軌包含在具有`default`標籤的音軌集合中。 替代音訊串流的中繼資料會包含在具有`TYPE=AUDIO`之`#EXT-X-MEDIA`標籤的播放清單中。

例如，指定多個替代音訊串流的M3U8資訊清單可能如下所示：

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

