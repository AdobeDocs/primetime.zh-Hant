---
description: 您可以選擇使用預設廣告行為。
title: 使用預設播放行為
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---


# 使用預設播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

要使用預設行為：

* 如果您實作自己的`ContentFactory`類別，請在`doRetrieveAdPolicySelector`的實作中傳回新的`DefaultAdPolicySelector`例項。

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

* 如果您沒有`ContentFactory`類別的自訂實作，TVSDK會使用`DefaultAdPolicySelector`。