---
description: 隱藏式字幕和字幕有一些獨特的差異，您可以透過不同的方式啟用它們。
title: 字幕和隱藏式字幕的需求
exl-id: f90dcfb7-4fd2-41d5-8396-cdc827f8a8c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 字幕和隱藏式字幕的需求 {#requirements-for-subtitles-and-closed-captions}

隱藏式字幕和字幕有一些獨特的差異，您可以透過不同的方式啟用它們。

字幕串流會與主要內容並行執行。 隱藏式字幕是MPEG-2視訊資料流資料封包的一部分。

請注意隱藏式字幕和字幕的下列需求：

* **隱藏式字幕**

   * 隱藏式字幕的語言通常與音訊相同，而且也會將背景聲音表示為文字。
   * 隱藏式字幕是視訊傳輸資料流中MPEG-2視訊資料封包的一部分。
   * 隱藏式字幕僅支援AV Foundation架構所提供的範圍。

* **字幕**

   * 字幕通常使用不同的語言，不包含背景音效。
   * 字幕位於與主要內容平行執行的串流中。

      此 `PTMediaPlayer` 播放主要內容和廣告，其中主要內容可能是即時/線性或VOD，廣告可能是前段、中段或後段。
   以下是iOS中字幕的額外需求：

   * 若為時間戳記，請 `X-TIMESTAMP-MAP` 值，該值是在的標頭區段中指定的 `WebVTT` 檔案，必須符合視訊時間戳記。

   * 對於系統，您必須使用iOS 6.1或更新版本。


>[!IMPORTANT]
>
>字幕需求不適用於隱藏式字幕。
