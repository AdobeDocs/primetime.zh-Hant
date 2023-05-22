---
description: MediaResource表示MediaPlayer實例將要載入的內容。
title: MediaPlayer和MediaResource類
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# MediaPlayer和MediaResource類{#mediaplayer-and-mediaresource-classes}

MediaResource表示MediaPlayer實例將要載入的內容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK庫提供了一種簡單的方法，通過使用 `replaceCurrentResource` 中 `MediaPlayer` 。 此方法接收的實例 `MediaResource` 類作為唯一輸入參數。 的 `MediaResource` 類由以下資訊組成：

* 一個URL，它表示要載入的內容的位置。
* 一種類型，即即將載入的內容類型。

   這是一個字串，它定義可由 `MediaPlayer`。 可能的值是HLS和HDS。 每個值都與表示常用檔案副檔名的字串關聯，HLS為「m3u8」，HDS為「f4m」。
* 某些元資料，是 `Metadata` 類。

   此類似字典的結構可能包含有關即將載入的內容的其他資訊，例如關於應放置在主內容中的替代/廣告內容的資訊。

元資料是將與備用內容相關的資訊傳遞到TVSDK的介質。 的 `Metadata` interface為泛型key-value儲存定義API，其中鍵和值都是純字串。
