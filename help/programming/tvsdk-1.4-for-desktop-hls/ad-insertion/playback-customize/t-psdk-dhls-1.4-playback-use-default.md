---
description: 您可以選擇使用預設的廣告行為。
title: 使用預設播放行為
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 使用預設播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設的廣告行為。

使用預設行為：

* 如果您實作自己的 `ContentFactory` 類別，傳回新實體 `DefaultAdPolicySelector` 在您的實作中 `doRetrieveAdPolicySelector`.

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
