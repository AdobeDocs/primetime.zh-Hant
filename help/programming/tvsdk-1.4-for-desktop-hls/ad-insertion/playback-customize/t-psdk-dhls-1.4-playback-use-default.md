---
description: 您可以選擇使用預設廣告行為。
title: 使用預設回放行為
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 使用預設回放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

要使用預設行為：

* 如果您實施自己的 `ContentFactory` 類，返回新實例 `DefaultAdPolicySelector` 執行中 `doRetrieveAdPolicySelector`。

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

* 如果沒有自定義實現 `ContentFactory` 類， TVSDK使用 `DefaultAdPolicySelector`。
