---
description: 您可以自訂或覆寫廣告行為。
seo-description: 您可以自訂或覆寫廣告行為。
seo-title: 設定自訂播放
title: 設定自訂播放
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# 設定自訂播放{#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在自訂或覆寫廣告行為之前，請先向註冊廣告原則例項。
若要自訂廣告行為，請執行下列其中一項作業：

* 實施`AdPolicySelector`介面及其所有方法。

   如果您需要覆寫&#x200B;**all**&#x200B;預設廣告行為，建議使用此選項。

* 擴充`DefaultAdPolicySelector`類別，並僅提供需要自訂的行為實作。

   如果您只需要覆寫預設行為的&#x200B;**some**，建議使用此選項。

對於這兩個選項，請完成下列任務：

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
   >如果自訂內容工廠已通過`MediaPlayerItemConfig`類註冊特定流，則當取消分配`MediaPlayer`實例時將清除它。 每次建立新的播放作業時，您的應用程式都必須註冊它。