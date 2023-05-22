---
description: 廣告解析和廣告載入可能導致等待播放開始的用戶的不可接受的延遲。 懶惰廣告載入解析功能可減少此啟動延遲。 廣告現在可以在廣告中斷位置之前的指定間隔內解析。 這是通過使用雙玩家方法實現的。
title: 及時和解決
exl-id: dd5342c5-9f34-4778-a47a-91ff2eb03155
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 及時和解決 {#just-in-time-ad-resolving}

廣告解析和廣告載入可能導致等待播放開始的用戶的不可接受的延遲。 懶惰廣告載入解析功能可減少此啟動延遲。 廣告現在可以在廣告中斷位置之前的指定間隔內解析。 這是通過使用雙玩家方法實現的。

**基本的和解析和載入過程：**

1. TVSDK下載清單（播放清單）和 *解析* 所有廣告。
1. TVSDK *載荷* 所有廣告，並將廣告片段縫入艙單。
1. TVSDK將播放器移入PREPARED狀態，然後開始內容回放。

播放器使用清單中的URL來獲取廣告內容（創意），確保廣告內容是TVSDK可以播放的格式，並且TVSDK將廣告放在時間線上。 解析和載入廣告的這一基本過程可能導致等待播放其內容的用戶出現不可接受的長時間延遲，特別是當清單包含多個廣告URL時。

**懶惰廣告解決：**

1. TVSDK下載播放清單。
1. TVSDK *解析和載入* 任何預播廣告，將播放器移入PREPARED狀態，然後開始內容回放。
1. TVSDK *解析* 每個廣告在其位置之前破折，其位置基於在 `PTAdMetadata::delayAdLoadingTolerance`。

例如，預設情況下 `delayAdLoadingTolerance` 設定為5秒。 如果AdBreak設定為在3:00播放，則將在2時解決:55:00。 如果您認為廣告解析度需要超過5秒，則可能希望增加此值。

>[!IMPORTANT]
>
>**懶惰廣告解決時要考慮的因素：**
>* 只有SERVER_MAP和信令模式下的VOD流才支援懶惰Ad Resoling。
>* 預設情況下未啟用懶惰廣告解析。 必須設定 `PTAdMetadata::delayAdLoading` =是，啟用它。
>* 懶惰廣告解析與「即時開啟」功能不相容。 有關「即時開啟」的詳細資訊，請參見 [即時開啟](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)。
>* 懶惰廣告解析不支援「畫中畫」模式。 如果啟用「懶惰廣告解析」，請禁用任何「圖片中」模式。
>* 懶惰的廣告解析度不會影響預播廣告。
>

**啟用延遲和解析**

可以使用現有的懶惰廣告載入機制啟用或禁用懶惰廣告解析功能（預設情況下禁用懶惰廣告解析）。

可以通過設定 `PTAdMetadata::delayAdLoading`=設定廣告元資料時為「是」。

**與懶惰廣告解析相關的API:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
