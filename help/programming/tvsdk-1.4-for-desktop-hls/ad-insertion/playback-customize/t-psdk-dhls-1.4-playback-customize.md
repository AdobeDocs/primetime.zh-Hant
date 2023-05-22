---
description: 您可以自定義或覆蓋廣告行為。
title: 設定自定義播放
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 設定自定義播放{#set-up-customized-playback}

您可以自定義或覆蓋廣告行為。

在可以自定義或覆蓋廣告行為之前，請向註冊廣告策略實例。
要自定義廣告行為，請執行以下操作之一：

* 實施 `AdPolicySelector` 介面及其所有方法。

   如果需要覆蓋，建議使用此選項 **全部** 預設廣告行為。

* 擴展 `DefaultAdPolicySelector` 類並僅為那些需要自定義的行為提供實現。

   如果僅需要覆蓋，建議使用此選項 **有** 的子菜單。

對於這兩個選項，請完成以下任務：

1. 實施您自己的自定義廣告策略選擇器。

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. 擴展內容工廠以使用自定義廣告策略選擇器。

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. 註冊要由TVSDK在廣告工作流中使用的新內容工廠。

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >如果已通過為特定流註冊了自定義內容工廠 `MediaPlayerItemConfig` 類，在 `MediaPlayer` 實例被取消分配。 每次建立新的回放會話時，應用程式都必須註冊它。
