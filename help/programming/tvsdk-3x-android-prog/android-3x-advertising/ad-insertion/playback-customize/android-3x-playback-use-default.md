---
description: 您可以選擇使用預設廣告行為。
title: 使用預設回放行為
exl-id: 0ea3d2bb-b4d4-4090-ab5f-b6c31c1abe32
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 使用預設回放行為 {#use-the-default-playback-behavior}

您可以選擇使用預設廣告行為。

1. 要使用預設行為，請完成以下任務之一：

   * 如果您實施自己的 `AdvertisingFactory` 類，返回空 `createAdPolicySelector`。

   * 如果沒有自定義實現 `AdvertisingFactory` 類，TVSDK使用預設的廣告策略選擇器。

## 設定自定義播放 {#set-up-customized-playback}

您可以自定義或覆蓋廣告行為。

在可以自定義或覆蓋廣告行為之前，請向註冊廣告策略實例。
要自定義廣告行為，請執行以下操作之一：

* 實施 `AdPolicySelector` 介面及其所有方法。

   如果需要覆蓋，建議使用此選項 **全部** 預設廣告行為。

* 擴展 `DefaultAdPolicySelector` 類並僅為那些需要自定義的行為提供實現。

   如果僅需要覆蓋，建議使用此選項 **有** 的子菜單。

要自定義廣告行為：

1. 實施 `AdPolicySelector` 介面及其所有方法。
1. 通過廣告工廠分配TVSDK要使用的策略實例。

   >[!NOTE]
   >
   >類CustomContentFactory擴展了ContentFactory &amp;lbrace;
   >...
   >@Override
   >公共AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem)&amp;lbrace;
   >返回新的CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rbrace;
   >...
   >&amp;rbrace;
   >//使用媒體播放器註冊自定義內容工廠
   >MediaPlayerItemConfig =新的MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >//此配置應稍後在載入>資源時傳遞
   >mediaPlayer.replaceCurrentResource(resource, config);

1. 實施您的自定義。
