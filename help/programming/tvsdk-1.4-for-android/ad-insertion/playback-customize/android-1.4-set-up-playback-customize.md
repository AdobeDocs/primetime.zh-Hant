---
description: 您可以自定義或覆蓋廣告行為。
title: 設定自定義播放
exl-id: aaa4d1c2-c425-4a2e-8377-0a3072f3fb18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 設定自定義播放 {#cset-up-customized-playback}

通過向TVSDK註冊廣告策略實例，可以自定義或覆蓋廣告行為。

要自定義廣告行為，請執行以下操作之一：

* 實施 `AdPolicySelector` 介面及其所有方法。
如果需要覆蓋所有預設廣告行為，建議使用此選項。

* 擴展 `DefaultAdPolicySelector` 類並僅為那些需要自定義的行為提供實現。
如果只需要覆蓋某些預設行為，則建議使用此選項。

對於這兩個選項，請完成以下任務：

要自定義廣告行為：

1. 實現AdPolicySelector介面及其所有方法。

1. 通過廣告工廠分配TVSDK要使用的策略實例。

>[!IMPORTANT]
>
>當MediaPlayer實例>取消分配時，會清除在>回放開始處註冊的自定義廣告策略。每次建立新的回放會話時，應用程式都必須註冊一個策略>selector實例。

例如：

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. 實施您的自定義。
