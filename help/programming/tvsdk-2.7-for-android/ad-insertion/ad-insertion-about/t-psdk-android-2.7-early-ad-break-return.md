---
description: 對於直播串流廣告插入，您可能需要從廣告插播結束，然後播放插播中的所有廣告直到完成。
title: 實施提早的廣告插播回報
exl-id: 3c61f34f-3587-40c2-b480-4734b4cf9aef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 實施提早的廣告插播回報  {#implement-an-early-ad-break-return}

對於直播串流廣告插入，您可能需要從廣告插播結束，然後播放插播中的所有廣告直到完成。

例如，在廣告插播開始之前，某些體育賽事中的廣告插播持續時間可能並不知道。 TVSDK會提供預設持續時間，但如果遊戲在插播完成前繼續，則必須結束廣告插播。 另一個範例是即時資料流中廣告插播期間的緊急訊號。

1. 訂閱 `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`，即標籤中的接合輸出/接合。

   如需如何拼接/插入廣告標籤的詳細資訊，請參閱 [機會產生器和內容解析器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

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

   如需關於使用自訂的詳細資訊 `ContentFactory`，請參閱中的步驟1 [實作自訂機會產生器](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. 在相同自訂上 `ContentFactory`，實作 `retrieveResolvers` 並包含 `AuditudeResolver` 和 `SpliceInCustomResolver`.

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
