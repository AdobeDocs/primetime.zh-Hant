---
description: 您可以實作介面PlacementOpportunityDetector，來實作您自己的機會檢測器。
seo-description: 您可以實作介面PlacementOpportunityDetector，來實作您自己的機會檢測器。
seo-title: 實作自訂機會偵測器
title: 實作自訂機會偵測器
uuid: 012527c5-4ef0-4cd6-a9df-2fb861078a7e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 2%

---


# 實作自訂機會檢測器{#implement-a-custom-opportunity-detector}

您可以實作介面PlacementOpportunityDetector，來實作您自己的機會檢測器。

1. 建立自訂`AdvertisingFactory`例項並覆寫`createOpportunityDetector`。 例如：

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

1. 向`MediaPlayer`註冊廣告客戶端工廠。 例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 建立可擴展`PlacementOpportunityDetector`類的自定義機會檢測器類。
   1. 在自訂機會檢測器中，覆寫此函式：

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      `timedMetadataList`包含可用`TimedMetadata`的清單，該清單已排序。 中繼資料包含要傳送給廣告提供者的定位參數和自訂參數。

   1. 對於每個`TimedMetadata`，建立`List<PlacementOpportunity>`。 清單可以是空的，但不能是空的。 `PlacementOpportunity` 應具有下列屬性：

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. 為所有檢測到的定時元資料對象建立放置機會後，只需返回`PlacementOpportunity`清單。

這是自訂位置機會檢測器範例：

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

