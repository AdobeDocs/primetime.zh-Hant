---
description: 您可以選擇使用預設廣告行為。
title: 使用預設播放行為
exl-id: eb4ce0b4-9dfd-4de8-8cbf-8aba093a5ddd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用預設播放行為  {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 若要使用預設行為，請完成下列其中一項工作：

   * 如果您實作自己的 `AdvertisingFactory` 類別，傳回null `createAdPolicySelector`.

   * 如果您沒有的自訂實作 `AdvertisingFactory` 類別，TVSDK會使用預設的廣告原則選擇器。

## 設定自訂播放 {#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在您自訂或覆寫廣告行為之前，請先使用TVSDK註冊廣告原則執行個體。

* 實作 `AdPolicySelector` 介面及其所有方法。

   如果您需要覆寫，建議使用此選項 **全部** 預設廣告行為。

* 擴充 `DefaultAdPolicySelector` 類別並提供僅用於需要自訂之行為的實作。

   如果您只需要覆寫，則建議使用此選項 **部分** 預設行為的ID。

若要自訂廣告行為：

1. 實作 `AdPolicySelector` 介面及其所有方法。
1. 透過Advertising Factory指派TVSDK使用的原則執行個體。

   >[!NOTE]
   >
   >播放開始時註冊的自訂廣告原則會在以下情況下清除： `MediaPlayer` 執行個體已取消配置。 您的應用程式必須在每次建立新播放工作階段時註冊原則選擇器執行個體。

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

1. 實作您的自訂。
