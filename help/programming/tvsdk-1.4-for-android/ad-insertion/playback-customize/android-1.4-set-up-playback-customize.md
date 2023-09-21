---
description: 您可以自訂或覆寫廣告行為。
title: 設定自訂播放
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# 設定自訂播放 {#cset-up-customized-playback}

您可以在TVSDK註冊廣告原則執行個體，以自訂或覆寫廣告行為。

若要自訂廣告行為，請執行下列任一項作業：

* 實作 `AdPolicySelector` 介面及其所有方法。
如果您需要覆寫所有預設廣告行為，建議使用此選項。

* 擴充 `DefaultAdPolicySelector` 類別並提供僅用於需要自訂之行為的實作。
如果您只需要覆寫部分預設行為，則建議使用此選項。

針對這兩個選項，請完成下列作業：

若要自訂廣告行為：

1. 實作AdPolicySelector介面及其所有方法。

1. 透過廣告工廠指派TVSDK使用的原則執行個體。

>[!IMPORTANT]
>
>當MediaPlayer例項取消配置時，在播放開頭註冊的自訂廣告原則會被清除。您的應用程式必須在每次建立新播放工作階段時註冊原則選取器例項。

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

1. 實施您的自訂。
