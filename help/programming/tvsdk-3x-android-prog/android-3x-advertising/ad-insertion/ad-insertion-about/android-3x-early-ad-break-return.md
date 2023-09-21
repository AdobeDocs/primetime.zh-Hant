---
description: 針對即時串流廣告插入，您可能需要從廣告插播結束，然後才會播放插播中的所有廣告直到結束。
title: 實作提早的廣告插播回報
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 實作提早的廣告插播回報 {#implement-an-early-ad-break-return}

針對即時串流廣告插入，您可能需要從廣告插播結束，然後才會播放插播中的所有廣告直到結束。

例如，某些體育活動中的廣告插播持續時間可能無法在插播開始前知道。 TVSDK提供預設持續時間，但如果遊戲在插播完成前繼續，則必須結束廣告插播。 另一個範例是即時資料流中廣告插播期間的緊急訊號。

1. 訂閱 `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`，即標籤中的接合輸出/接合。
如需如何分割/嵌入廣告標籤的詳細資訊，請參閱 [機會產生器和內容解析器](../../ad-insertion/content-resolver/android-3x-content-resolver.md).
1. 使用自訂 `ContentFactory`.
1. 在 `retrieveGenerators`，使用 `SpliceInPlacementOpportunityGenerator`.

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   如需關於使用自訂的詳細資訊 `ContentFactory`，請參閱中的步驟1 [實施自訂機會產生器](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md).

1. 在相同自訂上 `ContentFactory`，實作 `retrieveResolvers` 並包含 `AuditudeResolver` 和 `SpliceInCustomResolver`.

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
