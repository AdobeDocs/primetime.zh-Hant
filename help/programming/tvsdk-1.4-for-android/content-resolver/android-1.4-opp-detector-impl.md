---
description: 通過實現介面PlacementOpportunityDetector，您可以實施您自己的機會檢測器。
title: 實施自定義機會檢測器
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 實施自定義機會檢測器 {#implement-a-custom-opportunity-detector}

通過實現介面PlacementOpportunityDetector，您可以實施您自己的機會檢測器。

1. 建立自定義 `AdvertisingFactory` 實例和覆蓋 `createOpportunityDetector`。 例如：

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. 將廣告客戶端工廠註冊到 `MediaPlayer`。 例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 建立自定義機會檢測器類，以擴展 `PlacementOpportunityDetector` 類。
   1. 在自定義機會檢測器中，覆蓋以下功能：

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      的 `timedMetadataList` 包含可用清單 `TimedMetadata`的子菜單。 元資料包含要發送到廣告提供程式的目標參數和自定義參數。

   1. 每個 `TimedMetadata`，建立 `List<PlacementOpportunity>`。 清單可以為空，但不能為空。 `PlacementOpportunity` 應具有以下屬性：

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 為檢測到的所有定時元資料對象建立放置機會後，只需返回 `PlacementOpportunity` 清單框。

這是一個示例自定義放置機會檢測器：

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```
