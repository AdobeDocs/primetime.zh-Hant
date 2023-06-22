---
description: 您可以選擇使用預設廣告行為。
title: 使用預設播放行為
exl-id: 8d25e076-4335-49c8-b6b8-f2694b1b9074
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 使用預設播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

若要使用預設行為：

* 如果您實作自己的 `ContentFactory` 類別，傳回新的執行個體 `DefaultAdPolicySelector` 在您的實作中 `doRetrieveAdPolicySelector`.

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

* 如果您沒有的自訂實作 `ContentFactory` 類別，TVSDK使用 `DefaultAdPolicySelector`.
