---
description: 你可以實施你自己的機會檢測器。
title: 實施自定義機會檢測器
exl-id: a3f6d6b3-4d5e-49bc-b8de-a1196305bbb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 實施自定義機會檢測器{#implement-a-custom-opportunity-detector}

你可以實施你自己的機會檢測器。

* 如果您的機會生成器基於 `TimedMetadata` 與當前媒體流關聯的對象，則應擴展 `SpliceOutOpportunityGenerator` 或 `TimedMetadataOpportunityGenerator`。

* 如果您的機會生成器基於由外部服務（如CIS）提供的帶外資料，則應擴展 `OpportunityGenerator`。

1. 建立自定義機會生成器。

       如果您的自定義機會生成器基於「TimedMetadata」對象，則擴展「TimedMetadataOpportunityGenerator」並覆蓋以下方法：
   
   * `doConfigure`  — 在建立媒體播放器項目後調用此方法，並提供機會生成器以根據需要建立初始機會集
   * `doProcess`  — 每次新建時都調用此方法 `TimedMetadata` 檢測到（例如，對於每次播放清單/清單刷新時的即時/線性流）

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

1. 建立使用自定義機會生成器的自定義內容工廠。

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

1. 為要播放的媒體流註冊自定義內容工廠。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
