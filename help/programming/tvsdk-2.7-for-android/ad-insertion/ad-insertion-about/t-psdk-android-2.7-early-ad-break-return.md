---
description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
title: 實施早期廣告插播傳回
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# 實作早期廣告插播傳回{#implement-an-early-ad-break-return}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

例如，某些體育賽事中的廣告分段持續時間在分段開始前可能不為人知。 TVSDK提供預設持續時間，但如果遊戲在中斷結束前繼續，則必須退出廣告中斷。 另一個例子是即時串流中廣告中斷期間的緊急訊號。

1. 訂閱`#EXT-X-CUE-OUT`、`#EXT-X-CUE-IN`和`#EXT-X-CUE`，它們是標籤中的剪接／剪接。

   有關如何剪接／插入廣告標籤的詳細資訊，請參見[Opportunity生成器和內容解析器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md)。

1. 使用自訂`ContentFactory`。
1. 在`retrieveGenerators`中，使用`SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有關使用自定義`ContentFactory`的詳細資訊，請參閱[實施自定義業務機會gerenator](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md)中的步驟1。

1. 在相同的自訂`ContentFactory`上，實作`retrieveResolvers`並包含`AuditudeResolver`和`SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

