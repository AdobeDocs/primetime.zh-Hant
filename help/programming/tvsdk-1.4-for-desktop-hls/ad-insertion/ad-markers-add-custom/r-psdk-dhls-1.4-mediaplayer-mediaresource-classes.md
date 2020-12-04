---
description: MediaResource代表MediaPlayer例項即將載入的內容。
seo-description: MediaResource代表MediaPlayer例項即將載入的內容。
seo-title: MediaPlayer和MediaResource類
title: MediaPlayer和MediaResource類
uuid: 36ef75f3-08f7-4fc5-88a7-9bab9198b917
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# MediaPlayer和MediaResource類{#mediaplayer-and-mediaresource-classes}

MediaResource代表MediaPlayer例項即將載入的內容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK程式庫提供簡單的方式，讓您使用`MediaPlayer`介面中的`replaceCurrentResource`方法來載入並準備內容以供播放。 此方法接收`MediaResource`類的實例作為唯一輸入參數。 `MediaResource`類由以下資訊組成：

* 一個URL，它代表即將載入之內容的位置。
* 一種類型，即即將載入的內容類型。

   此字串定義`MediaPlayer`可載入的內容類型。 可能的值是HLS和HDS。 每個值都與代表常用副檔名的字串關聯，即HLS的&quot;m3u8&quot;和HDS的&quot;f4m&quot;。
* 某些元資料，它是`Metadata`類的實例。

   此類似字典的結構可能包含有關即將載入內容的其他資訊，例如應放置在主要內容中的替代／廣告內容的資訊。

中繼資料是傳遞至TVSDK之替代內容相關資訊的媒介。 `Metadata`介面會定義一般金鑰值存放區的API，其中金鑰和值都是純字串。
