---
description: MediaResource代表即將由MediaPlayer例項載入的內容。
title: MediaPlayer和MediaResource類別
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# MediaPlayer和MediaResource類別{#mediaplayer-and-mediaresource-classes}

MediaResource代表即將由MediaPlayer例項載入的內容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK程式庫提供簡單方法，讓您載入及準備內容以供播放，方法是使用 `replaceCurrentResource` 中的方法 `MediaPlayer` 介面。 此方法接收 `MediaResource` 類別作為唯一的輸入引數。 此 `MediaResource` class由下列資訊組成：

* URL，代表即將載入之內容的位置。
* 型別，即將載入的內容型別。

   這是字串，定義可由 `MediaPlayer`. 可能的值包括HLS和HDS。 每個值都與代表常用副檔名的字串相關聯，「m3u8」代表HLS，「f4m」代表HDS。
* 部分中繼資料，這是 `Metadata` 類別。

   此類似字典的結構可能包含即將載入之內容的額外資訊，例如應放置在主要內容中的替代/廣告內容的資訊。

中繼資料是將與替代內容相關的資訊傳遞至TVSDK的媒體。 此 `Metadata` 介面會定義一般金鑰值存放區的API，其中金鑰和值都是純字串。
