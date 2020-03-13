---
description: 廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。
seo-description: 廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。
seo-title: 插入廣告
title: 插入廣告
uuid: 6e31cae5-7363-454f-82dd-e03c1e34cd3f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 插入廣告 {#insert-ads}

廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。

包含 *`ad break`* 依序播放的一或多個廣告。 TVSDK會將廣告插入主要內容中，作為一個或多個廣告插播的成員。

>[!TIP]
>
>如果廣告有錯誤，TVSDK會忽略廣告。

## 解析並插入VOD廣告 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支援數個VOD廣告解析與插入的使用案例。

* 前段廣告插入，廣告插入在內容開頭。
* 中段廣告插入，其中至少一個廣告插入內容的中間。
* 滾動後廣告插入，其中至少有一個廣告附加在內容的結尾。

TVSDK會解析廣告、將廣告插入廣告伺服器所定義的位置，並在播放開始前計算虛擬時間軸。 播放開始後，不會發生任何變更，例如插入的廣告或移除的插入廣告。

## 解析並插入即時和線性廣告 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支援即時和線性廣告解析與插入的數個使用案例。

* 前滾廣告插入，其中至少一個廣告插入在內容的開頭。
* 中段廣告插入，其中至少一個廣告插入內容的中間。

TVSDK會解析廣告，並在即時或線性串流中遇到提示點時插入廣告。 依預設，TVSDK支援在解析和放置廣告時，以下提示為有效的廣告標籤：

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

這些標籤需要中繼資料欄位 `DURATION` 的秒數，以及提示的唯一ID。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

如需其他提示的詳細資訊，請參 [閱訂閱自訂標籤](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md)。

## 追蹤用戶端廣告 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK會自動追蹤VOD和即時／線性串流的廣告。

通知會用來通知您的應用程式廣告進度，包括廣告何時開始及何時結束的相關資訊。

## 實施早期廣告插播傳回 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

以下是早期廣告插播返回的一些範例：

* 特定體育賽事中廣告插播的持續時間。

   雖然提供預設持續時間，但如果遊戲在中斷結束前繼續，廣告中斷必須退出。
* 即時串流中廣告中斷期間的緊急信號。

透過資訊清單中的自訂標籤（稱為剪接入或提示輸入標籤），識別提早退出廣告插播的能力。 TVSDK可讓應用程式訂閱這些剪接入標籤，以提供剪接入機會。

* 若要將標 `#EXT-X-CUE-IN` 簽當做拼接機會，並實作早期廣告插播傳回：

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

* 要共用用於剪接和剪接的相同標籤：

1. 如果應用程式共用相同的提示來指示提示／剪接和提示／剪接，請擴充並實 `PTDefaultAdOpportunityResolver` 施該方 `preparePlacementOpportunity` 法。

   [!TIP]

   下列程式碼假設應用程式具有方法的實 `isCueInOpportunity` 作。

```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
```

1. 在實例上註冊擴展的機會解 `PTDefaultMediaPlayerClientFactory` 決程式。

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
