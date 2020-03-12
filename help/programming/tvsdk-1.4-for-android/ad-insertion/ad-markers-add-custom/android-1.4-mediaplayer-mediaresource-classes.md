---
description: MediaResource代表MediaPlayer例項即將載入的內容。
seo-description: MediaResource代表MediaPlayer例項即將載入的內容。
seo-title: MediaPlayer和MediaResource類
title: MediaPlayer和MediaResource類
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer和MediaResource類{#mediaplayer-and-mediaresource-classes}

MediaResource代表MediaPlayer例項即將載入的內容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK程式庫提供簡單的方式，讓您使用MediaPlayer介面中的方法來載 `replaceCurrentItem` 入和準備內容以播放。 此方法會接收MediaResource類別的例項作為唯一輸入引數。 MediaResource類由以下資訊組成：

* 一個URL，它代表即將載入之內容的位置。
* 一種類型，即即將載入的內容類型。

   這是類中的簡單列舉， `MediaResource` 可定義MediaPlayer可載入的內容類型。 可能的值是HLS和HDS。 每個值都與代表HLS和HDS常用副檔名的字 `m3u8` 串相 `f4m` 關聯。
* 有些中繼資料，是類別的例 `Metadata` 項。

   此類似字典的結構可能包含有關即將載入內容的其他資訊，例如應放置在主要內容中的替代／廣告內容資訊。

中繼資料是傳遞至TVSDK之替代內容相關資訊的媒介。 介 `Metadata` 面會定義一般金鑰值存放區的API，其中金鑰和值都是純字串。
