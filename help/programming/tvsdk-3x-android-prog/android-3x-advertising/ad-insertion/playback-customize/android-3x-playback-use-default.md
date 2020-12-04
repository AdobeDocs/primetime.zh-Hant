---
description: 您可以選擇使用預設廣告行為。
seo-description: 您可以選擇使用預設廣告行為。
seo-title: 使用預設播放行為
title: 使用預設播放行為
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 使用預設的播放行為{#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 若要使用預設行為，請完成下列任一項工作：

   * 如果您實作自己的`AdvertisingFactory`類，請傳回`createAdPolicySelector`的null。

   * 如果您沒有`AdvertisingFactory`類別的自訂實作，TVSDK會使用預設廣告原則選擇器。

## 設定自訂播放{#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在自訂或覆寫廣告行為之前，請先向註冊廣告原則例項。
若要自訂廣告行為，請執行下列其中一項作業：

* 實施`AdPolicySelector`介面及其所有方法。

   如果您需要覆寫&#x200B;**all**&#x200B;預設廣告行為，建議使用此選項。

* 擴充`DefaultAdPolicySelector`類別，並僅提供需要自訂的行為實作。

   如果您只需要覆寫預設行為的&#x200B;**some**，建議使用此選項。

若要自訂廣告行為：

1. 實施`AdPolicySelector`介面及其所有方法。
1. 指派TVSDK透過廣告廠使用的原則例項。

   >[!NOTE]
   >
   >classCustomContentFactory擴展了ContentFactory &amp;lbrace;
   >...
   >@Override
   >publicAdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem)&amp;lbrace;
   >傳回新的CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbraces;
   >...
   >&amp;rbraces;
   >//向媒體播放器註冊自訂內容工廠
   >MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// this config will belled passed while loading >resource
   >mediaPlayer.replaceCurrentResource(resource, config);

1. 實作您的自訂。
