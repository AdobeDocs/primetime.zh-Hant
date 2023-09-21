---
description: 您可以實作自己的機會偵測器。
title: 實作自訂機會偵測器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 實作自訂機會偵測器{#implement-a-custom-opportunity-detector}

您可以實作自己的機會偵測器。

* 如果您的機會產生器是根據 `TimedMetadata` 與目前媒體資料流相關聯的物件，則它應擴充 `SpliceOutOpportunityGenerator` 或 `TimedMetadataOpportunityGenerator`.

* 如果您的機會產生器是根據外部服務（例如CIS）提供的頻外資料，則它應擴充 `OpportunityGenerator`.

1. 建立自訂機會產生器。

       如果您的自訂機會產生器以「TimedMetadata」物件為基礎，請擴充「TimedMetadataOpportunityGenerator」並覆寫這些方法：
   
   * `doConfigure`  — 在建立媒體播放器專案後呼叫此方法，並提供機會產生器來視需要建立初始機會集
   * `doProcess`  — 每次新增時都會呼叫此方法 `TimedMetadata` 會偵測到（例如，對於即時/線性資料流，每當播放清單/資訊清單重新整理時）

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. 建立使用自訂機會產生器的自訂內容工廠。

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. 註冊要播放的媒體資料流的自訂內容處理站。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
