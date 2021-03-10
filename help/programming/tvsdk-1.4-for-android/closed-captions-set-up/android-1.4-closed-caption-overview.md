---
description: 當聲音聽不見或觀眾聽不到時，隱藏字幕會將視訊的音訊部分顯示為畫面上的文字。
title: 從可用字軌中選擇目前的字幕軌
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 概述{#work-with-closed-captions}

當聲音聽不見或觀眾聽不到時，隱藏字幕會將視訊的音訊部分顯示為畫面上的文字。

隱藏字幕通常與音訊使用相同的語言，並且會顯示文字的背景音效，但字幕通常使用不同的語言，而不包含背景音效。

TVSDK支援轉換下列格式：

* 608和708隱藏字幕，作為HLS上視頻傳輸流的一部分，作為MPEG-2視頻流中的資料包傳送。
* WebVTT標題檔案，這些檔案是從M3U8資訊清單檔案中參考，如HLS規格所定義。 它們會自動在Primetime播放器中做為隱藏字幕軌道使用。

您可以：

* 選取可用標題軌道作為目前軌道，並監聽表示其他可用軌道的事件。
* 使用`MediaPlayer`介面開啟或關閉（可見或不可見）關閉的字幕。
* 選取樣式選項，以決定底層視訊引擎呈現隱藏字幕的方式。 使用`MediaPlayerItem`介面來選擇字型或字型顏色等格式。
