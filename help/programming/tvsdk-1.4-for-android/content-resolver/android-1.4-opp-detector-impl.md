---
description: 您可以實作介面PlacementOpportunityDetector來實作自己的機會偵測器。
title: 實作自訂機會偵測器
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 實作自訂機會偵測器 {#implement-a-custom-opportunity-detector}

您可以實作介面PlacementOpportunityDetector來實作自己的機會偵測器。

1. 建立自訂 `AdvertisingFactory` 執行個體和覆寫 `createOpportunityDetector`. 例如：

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

1. 將廣告使用者端工廠註冊至 `MediaPlayer`. 例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 建立可延伸的自訂機會偵測器類別 `PlacementOpportunityDetector` 類別。
   1. 在自訂機會偵測器中，覆寫此函式：

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      此 `timedMetadataList` 包含可用清單 `TimedMetadata`，已排序。 中繼資料包含要傳送給廣告提供者的目標定位引數和自訂引數。

   1. 針對每個 `TimedMetadata`，建立 `List<PlacementOpportunity>`. 清單可以是空的，但不可以是Null。 `PlacementOpportunity` 應該具有下列屬性：

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 為所有偵測到的定時中繼資料物件建立位置機會後，只要傳回 `PlacementOpportunity` 清單。

這是自訂位置機會偵測器的範例：

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
