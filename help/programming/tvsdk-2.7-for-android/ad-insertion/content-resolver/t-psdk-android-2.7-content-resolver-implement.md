---
description: 您可以根據預設解析器實作您自己的內容解析器。
seo-description: 您可以根據預設解析器實作您自己的內容解析器。
seo-title: 建置自訂內容解析程式
title: 建置自訂內容解析程式
uuid: bc0eda17-9b5d-4733-8e93-790758e68df5
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 2%

---


# 實作自訂內容解析器{#implement-a-custom-content-resolver}

您可以根據預設解析器實作您自己的內容解析器。

當TVSDK產生新商機時，它會透過註冊的內容解析器重複，尋找能夠解決該商機的內容解析器。 選擇返回`true`的第一個以解決該機會。 如果沒有內容解析器，則會略過該機會。 由於內容解析程式通常是非同步的，因此當程式完成時，內容解析程式負責通知TVSDK。

1. 透過延伸`ContentFactory`介面並覆寫`retrieveResolvers`，實作您自己的自訂`ContentFactory`。

   例如：

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. 將`ContentFactory`註冊到`MediaPlayer`。

   例如：

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. 將`AdvertisingMetadata`物件傳遞至TVSDK，如下所示：
   1. 建立`AdvertisingMetadata`對象。
   1. 將`AdvertisingMetadata`對象保存到`MediaPlayerItemConfig`。

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. 建立可擴充`ContentResolver`類別的自訂廣告解析程式類別。
   1. 在自訂廣告解析程式中，覆寫`doConfigure`、`doCanResolve`、`doResolve`、`doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      從傳入`doConfigure`的項目取得`advertisingMetadata`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. 對於每個職位安排機會，建立一個`List<TimelineOperation>`。

      此範例`TimelineOperation`提供`AdBreakPlacement`的結構：

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. 解決廣告後，請呼叫下列其中一個函式：

      * 如果廣告解析成功，請在`ContentResolverClient`上呼叫`process(List<TimelineOperation> proposals)`和`notifyCompleted(Opportunity opportunity)`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * 如果廣告解析失敗，請在`ContentResolverClient`上呼叫`notifyResolveError`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         例如：

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

此範例自訂廣告解析程式可解決商機並提供簡單廣告：

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

