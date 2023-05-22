---
description: 隱藏字幕和字幕有一些獨特的差異，你可以用不同的方式啟用它們。
title: 字幕和隱藏字幕要求
exl-id: f90dcfb7-4fd2-41d5-8396-cdc827f8a8c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 字幕和隱藏字幕要求 {#requirements-for-subtitles-and-closed-captions}

隱藏字幕和字幕有一些獨特的差異，你可以用不同的方式啟用它們。

副標題流與主內容並行運行。 隱藏字幕是MPEG-2視頻流的資料包的一部分。

您應瞭解隱藏字幕和字幕的以下要求：

* **隱藏字幕**

   * 隱藏字幕通常與音頻使用相同的語言，並且還將背景聲音表示為文本。
   * 隱藏字幕是視頻傳輸流中MPEG-2視頻流的資料包的一部分。
   * 在AV Foundation框架提供的範圍內支援隱藏字幕。

* **字幕**

   * 字幕通常使用不同的語言，不包括背景音。
   * 字幕是與主內容並行運行的流。

      的 `PTMediaPlayer` 播放主要內容和廣告，主要內容可以是即時/線性或視頻點播，廣告可以是預卷、中卷或後卷。
   以下是iOS字幕的附加要求：

   * 對於時間戳， `X-TIMESTAMP-MAP` 值，在 `WebVTT` 檔案，必須與視頻時間戳匹配。

   * 對於系統，必須使用iOS6.1或更高版本。


>[!IMPORTANT]
>
>字幕要求不適用於隱藏字幕。
