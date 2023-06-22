---
description: 您可以自訂或覆寫廣告行為。
title: 設定自訂播放
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 設定自訂播放{#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在您可以自訂或覆寫廣告行為之前，請先使用註冊廣告原則執行個體。
若要自訂廣告行為，請執行下列任一項作業：

* 實作 `AdPolicySelector` 介面及其所有方法。

   如果您需要覆寫，建議使用此選項 **全部** 預設廣告行為。

* 擴充 `DefaultAdPolicySelector` 類別並提供僅用於需要自訂之行為的實作。

   如果您只需要覆寫，則建議使用此選項 **部分** 預設行為的ID。

針對這兩個選項，請完成下列工作：

1. 實作您自己的自訂廣告原則選擇器。

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. 擴充內容工廠以使用自訂廣告原則選擇器。

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

1. 註冊TVSDK在廣告工作流程中使用的新內容工廠。

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >如果自訂內容處理站是透過 `MediaPlayerItemConfig` 類別，則會在 `MediaPlayer` 執行個體已取消配置。 您的應用程式必須在每次建立新的播放工作階段時註冊它。
