---
description: 廣告解析和廣告載入可能會造成使用者等待播放開始時無法接受的延遲。 「延遲廣告載入解析」功能可降低此啟動延遲。 廣告現在可以在廣告插播位置之前的指定間隔內解決。 這是使用雙玩家方法實現的。
title: 即時廣告解決方案
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# 即時廣告解析{#just-in-time-ad-resolving}

廣告解析和廣告載入可能會造成使用者等待播放開始時無法接受的延遲。 「延遲廣告載入解析」功能可降低此啟動延遲。 廣告現在可以在廣告插播位置之前的指定間隔內解決。 這是使用雙玩家方法實現的。

**基本廣告解析與載入程式：**

1. TVSDK會下載資訊清單（播放清單）和&#x200B;*resolves*&#x200B;所有廣告。
1. TVSDK *會載入*&#x200B;所有廣告，並將廣告區段接合至資訊清單中。
1. TVSDK會將播放器移至「已準備」狀態，而內容播放便會開始。

播放器使用資訊清單中的URL來取得廣告內容（創作元素），確保廣告內容是TVSDK可播放的格式，而TVSDK會將廣告放在時間軸上。 這個解析和載入廣告的基本程式會造成使用者等待播放其內容時，尤其是資訊清單包含數個廣告URL時，無法接受的長時間延遲。

**懶惰廣告解決：**

1. TVSDK會下載播放清單。
1. TVSDK *解析並載入*&#x200B;任何前置廣告，將播放器移入PREPARED狀態，然後內容播放開始。
1. TVSDK *根據`PTAdMetadata::delayAdLoadingTolerance`中定義的值，解析每個廣告在其位置之前的中斷。*

例如，預設`delayAdLoadingTolerance`設定為5秒。 如果AdBreak設為在3:00播放，則會在2:55:00解決。 如果您認為廣告解析度需要超過5秒，您可能會想要增加此值。

>[!IMPORTANT]
>
>**使用懶惰廣告解決時要考慮的因素：**
>* 只有在模式為SERVER_MAP和信令模式時，才支援VOD流的延遲廣告解析。
>* 預設不會啟用「懶惰廣告解析」。 必須設定`PTAdMetadata::delayAdLoading` = YES才能啟用它。
>* 「懶惰廣告解析」與「立即啟動」功能不相容。 有關「立即啟動」的詳細資訊，請參見[「立即啟動」](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)。
>* 懶惰廣告解析不支援畫中畫模式。 如果您啟用「懶惰廣告解析」，請停用任何「畫中畫」模式。
>* 延遲廣告解析度不會影響前段廣告。

>


**啟用延遲廣告解析**

您可以使用現有的「延遲廣告載入」機制來啟用或停用「延遲廣告解析」功能（預設會停用「延遲廣告解析」）。

您可以在設定廣告中繼資料時，設定`PTAdMetadata::delayAdLoading`= YES，以啟用「懶惰廣告解析」。

**與延遲廣告解析度相關的API:**

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
