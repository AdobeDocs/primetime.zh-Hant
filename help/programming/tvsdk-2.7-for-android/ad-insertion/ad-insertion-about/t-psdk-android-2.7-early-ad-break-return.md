---
description: 對於即時流廣告插入，您可能需要先退出廣告分段，然後才能播放該分段中的所有廣告，直到完成。
title: 實施提前退貨
exl-id: 3c61f34f-3587-40c2-b480-4734b4cf9aef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 實施提前退貨  {#implement-an-early-ad-break-return}

對於即時流廣告插入，您可能需要先退出廣告分段，然後才能播放該分段中的所有廣告，直到完成。

例如，某些體育賽事的廣告中斷時間在中斷開始之前可能不知道。 TVSDK提供預設持續時間，但如果遊戲在中斷結束前恢復，則必須退出廣告中斷。 另一個示例是即時流中廣告中斷期間的緊急信號。

1. 訂閱 `#EXT-X-CUE-OUT`。 `#EXT-X-CUE-IN`, `#EXT-X-CUE`，即標籤中的剪接輸出/剪接。

   有關如何剪接/插入廣告標籤的詳細資訊，請參見 [機會生成器和內容解決器](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md)。

1. 使用自定義 `ContentFactory`。
1. 在 `retrieveGenerators`，使用 `SpliceInPlacementOpportunityGenerator`。

   例如：

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   有關使用自定義的詳細資訊 `ContentFactory`請參閱步驟1 [實施自定義機會生成器](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md)。

1. 在同一自定義上 `ContentFactory`執行 `retrieveResolvers` 包括 `AuditudeResolver` 和 `SpliceInCustomResolver`。

   例如：

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
