---
description: 您可以基於預設的解析器來實現解析器。
title: 實施自定義機會/內容解析器
exl-id: f2a8512f-9f6c-4fd9-8694-32132cddc7d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 實施自定義機會/內容解析器{#implement-a-custom-opportunity-content-resolver}

您可以基於預設的解析器來實現解析器。

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 通過擴展 `PTContentResolver` 抽象類。

   `PTContentResolver` 是必須由內容解析器類實現的介面。 同名的抽象類也可用，並自動處理配置（獲取代理）。

   >[!TIP]
   >
   >`PTContentResolver` 通過 `PTDefaultMediaPlayerClientFactory` 類。 客戶端可以通過擴展 `PTContentResolver` 抽象類。 預設情況下，除非特別刪除， `PTDefaultAdContentResolver` 在 `PTDefaultMediaPlayerClientFactory`。

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. 實施 `shouldResolveOpportunity` 返回 `YES` 如果它應處理接收的 `PTPlacementOpportunity`。
1. 實施 `resolvePlacementOpportunity`，即開始載入備用內容或廣告。
1. 載入廣告後，準備 `PTTimeline` 的子菜單。

       以下是一些有關時間表的有用資訊：
   
   * 可能有多個 `PTAdBreak`預卷、中卷和後卷類型。

      * A `PTAdBreak` 具有以下內容：

         * A `CMTimeRange` 開始時間和中斷時間。

            此屬性設定為 `PTAdBreak`。

         * `NSArray` 共 `PTAd`s

            此設定為 `PTAdBreak`。
   * A `PTAd` 代表廣告，每個 `PTAd` 具有以下內容：

      * A `PTAdHLSAsset` 設定為廣告的主要資產屬性。
      * 可能是多個 `PTAdAsset` 例如可點擊廣告或橫幅廣告。

   例如：

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. 呼叫 `didFinishResolvingPlacementOpportunity`，它提供 `PTTimeline`。
1. 通過調用將自定義內容/廣告解析程式註冊到預設媒體播放器工廠 `registerContentResolver`。

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 如果實施了自定義機會解析程式，請將其註冊到預設媒體播放器工廠。

   >[!TIP]
   >
   >您不必註冊自定義機會解析程式來註冊自定義內容/廣告解析程式。

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

當播放器載入內容並確定為VOD或LIVE類型時，發生以下情況之一：>
* 如果內容是VOD，則使用定制內容解析器來獲取整個視頻的廣告時間線。
* 如果內容是LIVE，則每次在內容中檢測到放置機會（提示點）時都調用自定義內容解析器。
