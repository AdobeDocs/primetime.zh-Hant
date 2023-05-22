---
description: 當聲音不可聽或觀眾聽不到時，關閉字幕將視頻的音頻部分作為文本顯示在螢幕上。
title: 使用隱藏字幕
exl-id: e93725e3-6c6d-42b8-83d0-0feb4f9be50b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 概述 {#work-with-closed-captions-overview}

當聲音不可聽或觀眾聽不到時，關閉字幕將視頻的音頻部分作為文本顯示在螢幕上。

隱藏字幕通常與音頻使用相同的語言，並且還顯示背景聲音與文本，但字幕通常使用不同的語言，不包括背景聲音。

TVSDK支援呈現以下格式：

* 608和708關閉字幕，當作MPEG-2視頻流中的資料包在HLS上傳輸時，它們作為視頻傳輸流的一部分被傳送。
* WebVTT標題檔案，這些檔案從M3U8清單檔案中引用，如HLS規範中所定義。

   這些檔案在黃金時段播放器中自動可用作隱藏字幕軌道。

您可以執行以下操作：

* 選擇一個可用字幕軌道作為當前字幕軌道，並偵聽指示其他可用字幕軌道的事件。
* 使用 `MediaPlayer` 。
* 選擇樣式選項，以指示底層視頻引擎如何呈現隱藏字幕。

   使用 `MediaPlayerItem` 的子菜單。
