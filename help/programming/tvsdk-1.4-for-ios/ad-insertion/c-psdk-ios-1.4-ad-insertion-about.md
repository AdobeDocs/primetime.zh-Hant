---
description: 廣告插入解析視訊點播(VOD) 、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。
title: 插入廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 插入廣告{#insert-ads}

廣告插入解析視訊點播(VOD) 、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。

一個 *`ad break`* 包含一或多個循序播放的廣告。 TVSDK會將廣告插入主要內容，作為一或多個廣告插播的成員。

>[!TIP]
>
>如果廣告發生錯誤，TVSDK會忽略廣告。

## 解析和插入VOD廣告 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支援數種VOD廣告解析和插入的使用案例。

* 前置式廣告插入，將廣告插入在內容的開頭。
* 中段廣告插入，其中至少一個廣告插入內容中間。
* 後置廣告插入，其中至少一個廣告附加在內容的結尾。

TVSDK會解析廣告、將廣告插入廣告伺服器定義的位置，並在播放開始之前計算虛擬時間軸。 播放開始後，不會發生任何變更，例如插入的廣告或移除的插入廣告。

## 解析並插入即時和線性廣告 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支援數種即時和線性廣告解析和插入的使用案例。

* 前置廣告插入，其中至少一個廣告插入在內容的開頭。
* 中段廣告插入，其中至少一個廣告插入內容中間。

TVSDK會在即時或線性資料流中遇到提示點時，解析廣告並插入廣告。 依預設，TVSDK在解析及放置廣告時，支援以下提示作為有效的廣告標籤：

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

這些標籤需要中繼資料欄位的 `DURATION` 秒數和提示的唯一ID。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

如需其他提示的詳細資訊，請參閱 [訂閱自訂標籤](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## 追蹤使用者端廣告 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK會自動追蹤VOD和即時/線性串流的廣告。

通知可用來通知應用程式廣告的進度，包括廣告何時開始和何時結束的資訊。

## 實作提早的廣告插播回報 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

針對即時串流廣告插入，您可能需要從廣告插播結束，然後才會播放插播中的所有廣告直到結束。

以下是早期廣告插播回訪的一些範例：

* 某些體育活動中的廣告插播持續時間。

  雖然已提供預設持續時間，但如果遊戲在插播完成前繼續，則必須結束廣告插播。
* 即時資料流中廣告插播期間的緊急訊號。

透過資訊清單中的自訂標籤（稱為接合或提示加入標籤）來識別及早退出廣告插播的功能。 TVSDK可讓應用程式訂閱這些接合標籤，以提供接合機會。

* 若要使用 `#EXT-X-CUE-IN` 標籤為插入式商機，並提前實作廣告插播回報：

   1. 訂閱標籤。

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 新增提示機會解析程式。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 要針對接合輸出和接合輸入共用相同的標籤：

   1. 如果應用程式共用相同的提示來指示提示輸出/接合輸出和提示輸入/接合輸入，請延伸 `PTDefaultAdOpportunityResolver` 並實作 `preparePlacementOpportunity` 方法。

      >[!TIP]
      >
      >下列程式碼假設應用程式針對下列專案實作： `isCueInOpportunity` 方法。
      >
      >```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```
      >

   1. 在上註冊擴充商機解析程式 `PTDefaultMediaPlayerClientFactory` 執行個體。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```
