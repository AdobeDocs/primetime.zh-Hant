---
description: 廣告插入解決了用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。
title: 插入廣告
exl-id: 94262bd5-3f8c-449d-934f-8177869707bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 插入廣告 {#insert-ads}

廣告插入解決了用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。

安 *`ad break`* 包含一個或多個按順序播放的廣告。 TVSDK將廣告作為一個或多個廣告分段的成員插入主內容中。

>[!TIP]
>
>如果廣告有錯誤，TVSDK將忽略該廣告。

## 解析和插入VOD廣告 {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK支援VOD廣告解析和插入的幾種使用情形。

* 預卷廣告插入，其中廣告在內容的開頭插入。
* 中間卷廣告插入，其中至少一個廣告被插入內容的中間。
* 滾動後廣告插入，其中至少一個廣告附加在內容的末端。

TVSDK解析廣告，在廣告伺服器定義的位置插入廣告，並在播放開始前計算虛擬時間軸。 播放開始後，不會發生任何更改，如插入廣告或刪除插入廣告。

## 解決並插入即時和線性廣告 {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK支援多種即時和線性廣告解析和插入使用案例。

* 預滾廣告插入，其中至少一個廣告插入在內容的開頭。
* 中間卷廣告插入，其中至少一個廣告被插入內容的中間。

TVSDK解析廣告，並在即時或線性流中遇到提示點時插入廣告。 預設情況下，TVSDK在解析和放置廣告時支援以下提示作為有效的廣告標籤：

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

這些標籤要求元資料欄位 `DURATION` 以秒為單位，提示的唯一ID。 例如：

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

有關其他提示的詳細資訊，請參見 [訂閱自定義標籤](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md)。

## 跟蹤客戶端廣告 {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK自動跟蹤視頻點播和即時/線性流播的廣告。

通知用於通知您的應用程式廣告進度，包括廣告何時開始和何時結束的資訊。

## 實施提前退貨 {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

對於即時流廣告插入，您可能需要先退出廣告分段，然後才能播放該分段中的所有廣告，直到完成。

下面是一些早期廣告時段返回的示例：

* 某些體育賽事廣告的時段。

   儘管提供了預設持續時間，但如果遊戲在中斷結束前恢復，則必須退出廣告中斷。
* 在即時流中廣告中斷期間的緊急信號。

通過清單中稱為剪接或提示標籤的定製標籤識別早期退出廣告中斷的能力。 TVSDK允許應用程式訂閱這些剪接入標籤以提供剪接入機會。

* 使用 `#EXT-X-CUE-IN` 標籤為插入機會，並實現早期的廣告分段返回：

   1. 訂閱標籤。

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. 添加提示入機會解析程式。

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* 要共用用於剪接和剪接的同一標籤：

1. 如果應用程式共用相同的提示以指示提示輸出/剪接和提示輸入/剪接輸入，則延伸 `PTDefaultAdOpportunityResolver` 並執行 `preparePlacementOpportunity` 的雙曲餘切值。

   >[!TIP]
   >
   >以下代碼假定應用程式具有 `isCueInOpportunity` 的雙曲餘切值。

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

1. 在上註冊擴展機會解析器 `PTDefaultMediaPlayerClientFactory` 實例。

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
