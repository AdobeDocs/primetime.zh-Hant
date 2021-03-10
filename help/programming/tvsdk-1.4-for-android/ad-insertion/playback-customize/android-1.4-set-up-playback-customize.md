---
description: 您可以自訂或覆寫廣告行為。
title: 設定自訂播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# 設定自訂播放{#cset-up-customized-playback}

您可以透過向TVSDK註冊廣告原則例項，自訂或覆寫廣告行為。

若要自訂廣告行為，請執行下列其中一項作業：

* 實施`AdPolicySelector`介面及其所有方法。
如果您需要覆寫所有預設廣告行為，建議使用此選項。

* 擴充`DefaultAdPolicySelector`類別，並僅提供需要的行為實作
自訂。
如果您只需要覆寫部分預設行為，建議使用此選項。

對於這兩個選項，請完成下列任務：

若要自訂廣告行為：

1. 實作AdPolicySelector介面及其所有方法。

1. 指派TVSDK透過廣告廠使用的原則例項。

>[!IMPORTANT]
>
>當MediaPlayer例項>deallocated時，會清除在>playback開頭註冊的自訂廣告原則。您的應用程式必須在每次建立新的播放作業時註冊原則>選擇器例項。

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

1. 實作您的自訂。