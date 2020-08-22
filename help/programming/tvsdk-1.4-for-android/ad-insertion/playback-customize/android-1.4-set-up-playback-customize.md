---
description: 您可以自訂或覆寫廣告行為。
seo-description: 您可以自訂或覆寫廣告行為。
seo-title: 設定自訂播放
title: 設定自訂播放
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# 設定自訂播放 {#cset-up-customized-playback}

您可以透過向TVSDK註冊廣告原則例項，自訂或覆寫廣告行為。

若要自訂廣告行為，請執行下列其中一項作業：

* 實作介 `AdPolicySelector` 面及其所有方法。
如果您需要覆寫所有預設廣告行為，建議使用此選項。

* 擴充類 `DefaultAdPolicySelector` 別，並僅針對需要自訂的行為提供實作。
如果您只需要覆寫部分預設行為，建議使用此選項。

對於這兩個選項，請完成下列任務：

若要自訂廣告行為：

1. 實作AdPolicySelector介面及其所有方法。

1. 指派TVSDK透過廣告廠使用的原則例項。

>[!IMPORTANT]
>
>當MediaPlayer例項>deallocated時，會清除在>playback開頭註冊的自訂廣告原則。您的應用程式必須在每次建立新的播放作業時，註冊一個原則>選擇器例項。

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