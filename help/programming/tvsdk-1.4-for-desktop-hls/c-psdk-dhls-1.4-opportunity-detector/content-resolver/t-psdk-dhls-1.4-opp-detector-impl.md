---
description: 您可以建置自己的機會檢測器。
title: 實作自訂機會偵測器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# 實作自訂機會檢測器{#implement-a-custom-opportunity-detector}

您可以建置自己的機會檢測器。

* 如果您的業務機會生成器基於與當前媒體流關聯的`TimedMetadata`對象，則應擴展`SpliceOutOpportunityGenerator`或`TimedMetadataOpportunityGenerator`。

* 如果您的業務機會生成器基於外部服務（如CIS）提供的帶外資料，則應擴展`OpportunityGenerator`。

1. 建立自訂商機產生器。

       如果您的自訂商機產生器是以「TimedMetadata」物件為基礎，請擴充「TimedMetadataOpportunityGenerator」並覆寫下列方法：
   
   * `doConfigure` -在建立媒體播放器項目後調用此方法，並提供機會生成器以建立初始的機會集（如果需要）
   * `doProcess` -每次偵測到新的時候都會 `TimedMetadata` 呼叫此方法（例如，每次播放清單／資訊清單重新整理時，即時／線性串流）

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

1. 建立自訂內容工廠，使用自訂商機產生器。

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

1. 註冊要播放的媒體串流的自訂內容工廠。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

