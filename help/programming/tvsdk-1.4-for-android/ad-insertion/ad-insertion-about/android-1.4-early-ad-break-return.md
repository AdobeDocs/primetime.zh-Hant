---
description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-title: 實施早期廣告插播傳回
title: 實施早期廣告插播傳回
uuid: 41b70ee1-290b-4732-899e-32b234ec1d9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 實施早期廣告插播傳回 {#implement-an-early-ad-break-return}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

例如，某些體育賽事中的廣告分段持續時間在分段開始前可能不為人知。 TVSDK提供預設持續時間，但如果遊戲在中斷結束前繼續，則必須退出廣告中斷。 另一個例子是即時串流中廣告中斷期間的緊急訊號。

1. 訂閱剪接出／插入廣告標籤( `#EXT-X-CUE-OUT`、 `#EXT-X-CUE-IN`和 `#EXT-X-CUE`)。

   如需如何剪接／加入廣告標籤的詳細資訊，請參閱 [Opportunity產生器和內容解析器](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md)。
1. 使用自訂 `ContentFactory`。
1. 在 `retrieveGenerators()`中，使用 `SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   如需使用自訂的詳細資訊，請參 `ContentFactory`閱實作自訂機會 [偵測器中的步驟1](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) 。

1. 在相同的自訂 `ContentFactory`上，實 `retrieveResolvers` 作並包含 `AuditudeResolver` 和 `SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

