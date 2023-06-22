---
description: 廣告解析和廣告載入可能會導致等待播放開始的使用者發生無法接受的延遲。 延遲廣告載入解決功能可減少此啟動延遲。 現在可以在廣告插播位置之前的指定間隔解析廣告。 這是透過使用雙人播放器方法來達成。
title: 即時廣告解析
exl-id: dd5342c5-9f34-4778-a47a-91ff2eb03155
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 即時廣告解析 {#just-in-time-ad-resolving}

廣告解析和廣告載入可能會導致等待播放開始的使用者發生無法接受的延遲。 延遲廣告載入解決功能可減少此啟動延遲。 現在可以在廣告插播位置之前的指定間隔解析廣告。 這是透過使用雙人播放器方法來達成。

**基本廣告解析和載入程式：**

1. TVSDK下載資訊清單（播放清單）和 *解析* 所有廣告。
1. TVSDK *載入* 所有廣告並將廣告區段拼接至資訊清單。
1. TVSDK會將播放器移至「已準備」狀態，並開始播放內容。

播放器會使用資訊清單中的URL來取得廣告內容（創意）、確保廣告內容採用TVSDK可以播放的格式，以及TVSDK將廣告放在時間軸上。 這種解析和載入廣告的基本程式可能會導致等待播放其內容的使用者延遲太長，令人無法接受，尤其是當資訊清單包含多個廣告URL時。

**延遲廣告解決：**

1. TVSDK會下載播放清單。
1. TVSDK *解析並載入* 任何前段廣告、將播放器移至「已準備」狀態，並開始播放內容。
1. TVSDK *解析* 每個廣告在其位置之前根據中定義的值中斷 `PTAdMetadata::delayAdLoadingTolerance`.

例如，預設為 `delayAdLoadingTolerance` 設為5秒。 如果AdBreak設定為3:00播放，則會在2解決:55:00. 如果您認為廣告解析度需要超過5秒的時間，您可能會想要增加此值。

>[!IMPORTANT]
>
>**考慮延遲廣告解決的因素：**
>* 延遲廣告解析僅支援具有模式SERVER_MAP和訊號模式的VOD串流。
>* 延遲廣告解析預設為未啟用。 您必須設定 `PTAdMetadata::delayAdLoading` =是，以啟用它。
>* 延遲廣告解析與立即開啟功能不相容。 如需「立即開啟」的詳細資訊，請參閱 [立即開啟](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* 延遲廣告解析不支援畫中畫模式。 如果您啟用「延遲廣告解析」，請停用任何「子母畫面」模式。
>* 延遲廣告解析度不會影響前段廣告。
>

**啟用延遲廣告解析**

您可以使用現有的延遲廣告載入機制來啟用或停用延遲廣告解析功能（預設會停用延遲廣告解析）。

您可以透過設定來啟用延遲廣告解決 `PTAdMetadata::delayAdLoading`=設定廣告中繼資料時為「是」。

**與延遲廣告解析度相關的API：**

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
