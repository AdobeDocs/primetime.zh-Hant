---
description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-title: 實施早期廣告插播傳回
title: 實施早期廣告插播傳回
uuid: c67f2158-5df4-458c-a27a-6329c5d26638
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 實施早期廣告插播傳回 {#implement-an-early-ad-break-return}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

例如，某些體育賽事中的廣告分段持續時間在分段開始前可能不為人知。 TVSDK提供預設持續時間，但如果遊戲在中斷結束前繼續，則必須退出廣告中斷。 另一個例子是即時串流中廣告中斷期間的緊急訊號。

1. 訂閱、 `#EXT-X-CUE-OUT`和 `#EXT-X-CUE-IN`，這 `#EXT-X-CUE`些是標籤中的剪接／剪接。

   如需如何剪接／加入廣告標籤的詳細資訊，請參閱 [Opportunity產生器和內容解析器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md)。

1. 使用自訂 `ContentFactory`。
1. 在 `retrieveGenerators`中，使用 `SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有關使用自定義的詳細信 `ContentFactory`息，請參閱實施自 [定義業務機會生成器中的步驟1](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md)。

1. 在相同的自訂 `ContentFactory`上，實 `retrieveResolvers` 作並包含 `AuditudeResolver` 和 `SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

