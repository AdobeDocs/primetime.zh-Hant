---
description: 您可以選擇使用預設廣告行為。
title: 使用預設回放行為
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用預設回放行為  {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 要使用預設行為，請完成以下任務之一：

   * 如果您實施自己的 `AdvertisingFactory` 類，返回空 `createAdPolicySelector`。

   * 如果沒有自定義實現 `AdvertisingFactory` 類，TVSDK使用預設的廣告策略選擇器。

## 設定自定義播放 {#set-up-customized-playback}

您可以自定義或覆蓋廣告行為。

在自定義或覆蓋廣告行為之前，請向TVSDK註冊廣告策略實例。

* 實施 `AdPolicySelector` 介面及其所有方法。

   如果需要覆蓋，建議使用此選項 **全部** 預設廣告行為。

* 擴展 `DefaultAdPolicySelector` 類並僅為那些需要自定義的行為提供實現。

   如果僅需要覆蓋，建議使用此選項 **有** 的子菜單。

要自定義廣告行為：

1. 實施 `AdPolicySelector` 介面及其所有方法。
1. 通過廣告工廠分配TVSDK要使用的策略實例。

   >[!NOTE]
   >
   >在播放開始時註冊的自定義廣告策略在 `MediaPlayer` 實例被取消分配。 每次建立新的回放會話時，應用程式都必須註冊策略選擇器實例。

   例如：

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. 實施您的自定義。
