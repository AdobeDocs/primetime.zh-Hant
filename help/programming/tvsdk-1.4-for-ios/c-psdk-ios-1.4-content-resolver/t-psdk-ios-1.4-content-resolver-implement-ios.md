---
description: 您可以根據預設解析器來實施解析器。
title: 實作自訂機會/內容解析程式
exl-id: f2a8512f-9f6c-4fd9-8694-32132cddc7d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 實作自訂機會/內容解析程式{#implement-a-custom-opportunity-content-resolver}

您可以根據預設解析器來實施解析器。

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. 透過延伸 `PTContentResolver` 抽象類別。

   `PTContentResolver` 是必須由內容解析程式類別實作的介面。 也可以使用具有相同名稱的抽象類別，並自動處理設定（取得委派）。

   >[!TIP]
   >
   >`PTContentResolver` 會透過 `PTDefaultMediaPlayerClientFactory` 類別。 使用者端可藉由擴充以下功能來註冊新的內容解析器： `PTContentResolver` 抽象類別。 根據預設，除非特別移除， `PTDefaultAdContentResolver` 已註冊於 `PTDefaultMediaPlayerClientFactory`.

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

1. 實作 `shouldResolveOpportunity` 和傳回 `YES` 是否應該處理收到的 `PTPlacementOpportunity`.
1. 實作 `resolvePlacementOpportunity`，會開始載入替代內容或廣告。
1. 載入廣告後，請準備 `PTTimeline` 包含要插入之內容的資訊。

       以下是一些關於時間軸的實用資訊：
   
   * 可以有多個 `PTAdBreak`前段、中段和後段型別的組合。

      * A `PTAdBreak` 具有下列專案：

         * A `CMTimeRange` 以及中斷的開始時間和持續時間。

            這會設定為以下專案的範圍屬性： `PTAdBreak`.

         * `NSArray` 之 `PTAd`s.

            此專案設定為的廣告屬性 `PTAdBreak`.
   * A `PTAd` 代表廣告，而且每個 `PTAd` 具有下列專案：

      * A `PTAdHLSAsset` 設為廣告的主要資產屬性。
      * 可能有多個 `PTAdAsset` 例項做為可點按廣告或橫幅廣告。

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

1. 呼叫 `didFinishResolvingPlacementOpportunity`，可提供 `PTTimeline`.
1. 透過呼叫，將您的自訂內容/廣告解析程式註冊到預設媒體播放器工廠 `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. 如果您實作自訂機會解析器，請將其註冊到預設的媒體播放器工廠。

   >[!TIP]
   >
   >您不需要註冊自訂機會解析程式即可註冊自訂內容/廣告解析程式。

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

當播放器載入內容，且經判斷為VOD或LIVE型別時，會發生下列其中一種情況：>
* 如果內容為VOD，自訂內容解析器會用於取得整個視訊的廣告時間軸。
* 如果內容為「即時」，則每次在內容中偵測到版位機會（提示點）時，都會呼叫自訂內容解析器。
