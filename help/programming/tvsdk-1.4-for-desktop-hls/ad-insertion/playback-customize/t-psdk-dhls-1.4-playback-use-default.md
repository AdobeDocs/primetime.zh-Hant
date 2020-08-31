---
description: 您可以選擇使用預設廣告行為。
seo-description: 您可以選擇使用預設廣告行為。
seo-title: 使用預設播放行為
title: 使用預設播放行為
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 使用預設播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

要使用預設行為：

* 如果您實作自己的 `ContentFactory` 類別，請傳回實作中 `DefaultAdPolicySelector` 的新例項 `doRetrieveAdPolicySelector`。

   ```
   public class CustomContentFactory extends ContentFactory { 
   
       //... 
       // your custom code for advertising classes 
       //... 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function  
         doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new DefaultAdPolicySelector(item); 
       } 
   }
   ```

* 如果您沒有類別的自訂實作， `ContentFactory` TVSDK會使用 `DefaultAdPolicySelector`。