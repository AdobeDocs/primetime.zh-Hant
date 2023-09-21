---
description: 您可以選擇使用預設的廣告行為。
title: 使用預設播放行為
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 使用預設播放行為 {#use-the-default-playback-behavior}

您可以選擇使用預設的廣告行為。

1. 若要使用預設行為，請完成下列其中一項工作：

   * 如果您實作自己的 `AdvertisingFactory` 類別，傳回空值 `createAdPolicySelector`.

   * 如果您沒有的自訂實作 `AdvertisingFactory` 類別，TVSDK會使用預設的廣告原則選取器。

## 設定自訂播放 {#set-up-customized-playback}

您可以自訂或覆寫廣告行為。

在您可以自訂或覆寫廣告行為之前，請先註冊廣告原則執行個體。
若要自訂廣告行為，請執行下列任一項作業：

* 實作 `AdPolicySelector` 介面及其所有方法。

  如果您需要覆寫，建議使用此選項 **全部** 預設廣告行為。

* 擴充 `DefaultAdPolicySelector` 類別並提供僅用於需要自訂之行為的實作。

  如果您只需要覆寫，則建議使用此選項 **部分** 預設行為的URL。

若要自訂廣告行為：

1. 實作 `AdPolicySelector` 介面及其所有方法。
1. 透過廣告工廠指派TVSDK使用的原則執行個體。

   >[!NOTE]
   >
   >類別CustomContentFactory擴充ContentFactory &amp;lbrace；
   >...
   >@Override
   >公用AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace；
   >傳回新的CustomAdPolicySelector(mediaPlayerItem)；
   >大括弧(&amp;R)；
   >...
   >大括弧(&amp;R)；
   >//向media player註冊自訂內容工廠
   >MediaPlayerItemConfig =新的MediaPlayerItemConfig()；
   >config.setAdvertisingFactory(new CustomContentFactory())；
   >//載入資源時，稍後應該傳遞此設定
   >mediaPlayer.replaceCurrentResource(resource， config)；

1. 實施您的自訂。
