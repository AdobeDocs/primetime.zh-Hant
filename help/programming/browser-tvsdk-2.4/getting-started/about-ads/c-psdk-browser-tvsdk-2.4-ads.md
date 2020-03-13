---
description: 當內容播放時，瀏覽器TVSDK可在建立MediaResource物件時顯示廣告並傳遞廣告相關資訊。
seo-description: 當內容播放時，瀏覽器TVSDK可在建立MediaResource物件時顯示廣告並傳遞廣告相關資訊。
seo-title: 廣告
title: 廣告
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 概觀 {#ads-overview}

當內容播放時，瀏覽器TVSDK可在建立MediaResource物件時顯示廣告並傳遞廣告相關資訊。

您可以選擇在收到函 `prepareToPlay` 數後呼叫函式 `AdobePSDK.MediaPlayerStatus.INITIALIZED`。

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

瀏覽器TVSDK也提供下列特定廣告事件，您可在事件處理常式中使用這些事件，以防止廣告播放時內容快速轉送：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

若要在UI Framework中檢視這項功能，請在設定中指定廣告設定，如下所示：

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

如需所需資訊的詳細資訊，請參 `AuditudeSettings`閱廣告 [插入中繼資料](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md)。
