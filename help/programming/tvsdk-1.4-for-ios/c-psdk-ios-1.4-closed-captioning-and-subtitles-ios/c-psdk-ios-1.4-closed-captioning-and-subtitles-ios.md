---
description: 隱藏式字幕和字幕有一些獨特的差異，您可以以不同的方式加以啟用。
title: 字幕和隱藏字幕
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 字幕和隱藏字幕的要求{#requirements-for-subtitles-and-closed-captions}

隱藏式字幕和字幕有一些獨特的差異，您可以以不同的方式加以啟用。

字幕流與主內容並行運行。 隱藏字幕是MPEG-2視頻流的資料包的一部分。

您應注意隱藏字幕和字幕的下列需求：

* **隱藏字幕**

   * 隱藏字幕通常與音訊使用相同的語言，也代表背景音效與文字。
   * 隱藏字幕是視頻傳輸流中MPEG-2視頻流的資料包的一部分。
   * 在AV Foundation架構提供的範圍內，隱藏字幕受到支援。

* **字幕**

   * 字幕通常使用不同的語言，不包含背景音效。
   * 字幕位於與主要內容平行執行的串流中。

      `PTMediaPlayer`會播放主要內容和廣告，其中主要內容可以是即時／線性或VOD，而廣告可以是前段、中段或後段。
   以下是iOS中字幕的其他需求：

   * 對於時間戳記，`X-TIMESTAMP-MAP`值（在`WebVTT`檔案的標題區段中指定）必須符合視訊時間戳記。

   * 對於系統，您必須使用iOS 6.1或更新版本。


>[!IMPORTANT]
>
>字幕的要求不適用於隱藏字幕。

