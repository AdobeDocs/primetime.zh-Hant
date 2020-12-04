---
description: 您可以選擇使用預設廣告行為。
seo-description: 您可以選擇使用預設廣告行為。
seo-title: 使用預設播放行為
title: 使用預設播放行為
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 使用預設的播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 若要使用預設行為，請完成下列任一項工作：

   * 如果您實作自己的`AdvertisingFactory`類，請傳回`createAdPolicySelector`的null。

   * 如果您沒有`AdvertisingFactory`類別的自訂實作，TVSDK會使用預設廣告原則選擇器。

## 設定自訂播放{#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在您自訂或覆寫廣告行為之前，請向TVSDK註冊廣告政策例項。

* 實施`AdPolicySelector`介面及其所有方法。

   如果您需要覆寫&#x200B;**all**&#x200B;預設廣告行為，建議使用此選項。

* 擴充`DefaultAdPolicySelector`類別，並僅提供需要自訂的行為實作。

   如果您只需要覆寫預設行為的&#x200B;**some**，建議使用此選項。

若要自訂廣告行為：

1. 實施`AdPolicySelector`介面及其所有方法。
1. 指派TVSDK透過廣告廠使用的原則例項。

   >[!NOTE]
   >
   >取消分配`MediaPlayer`實例時，會清除在播放開始時註冊的自定義廣告策略。 每次建立新的播放作業時，您的應用程式都必須註冊原則選擇器例項。

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