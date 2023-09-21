---
description: MediaResource代表即將由MediaPlayer例項載入的內容。
title: MediaPlayer和MediaResource類別
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# MediaPlayer和MediaResource類別{#mediaplayer-and-mediaresource-classes}

MediaResource代表即將由MediaPlayer例項載入的內容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK程式庫可讓您透過簡單的方式，載入及準備內容以供播放。 `replaceCurrentItem` MediaPlayer介面中的方法。 此方法會接收MediaResource類別的執行個體作為唯一的輸入引數。 MediaResource類別包含下列資訊：

* URL，代表即將載入之內容的位置。
* 型別，即將載入的內容型別。

  這是中的簡單列舉 `MediaResource` 類別來定義MediaPlayer可載入的內容型別。 可能的值包括HLS和HDS。 每個值都與代表常用副檔名的字串相關聯， `m3u8` 適用於HLS和 `f4m` 適用於HDS。
* 某些中繼資料，這是 `Metadata` 類別。

  此類似字典的結構可能包含即將載入內容的其他相關資訊，例如應該放置在主要內容中的替代/廣告內容相關資訊。

中繼資料是將與替代內容相關的資訊傳遞至TVSDK的媒體。 此 `Metadata` 介面會定義一般金鑰值存放區的API，其中金鑰和值都是純字串。
