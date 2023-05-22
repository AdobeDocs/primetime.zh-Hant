---
description: 瀏覽器TVSDK提供了建立高級視頻播放器應用程式（您的Mogki時播放器）的工具，您可以將其與其他Mogki時段元件整合。
title: Flash故障轉移
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Flash故障轉移 {#flash-failover}

瀏覽器TVSDK提供了建立高級視頻播放器應用程式（您的Mogki時播放器）的工具，您可以將其與其他Mogki時段元件整合。

使用平台的工具建立播放器並將其連接到瀏覽器TVSDK中的媒體播放器視圖，該視圖具有播放和管理視頻的方法。 例如，Browser TVSDK提供播放和暫停方法。 您可以在平台上建立用戶介面按鈕，並設定按鈕以調用這些瀏覽器TVSDK方法。

## Flash回退 {#section_92D3884A13A6431F9A9CC5C79715D888}

在瀏覽器TVSDK中，您的應用程式僅與 `Primetime.js` API。 基礎的瀏覽器TVSDK實現基於當前平台和要播放的媒體的資源類型來決定要使用的播放器技術。

在您致電之前，不會對播放器技術做出決定 `MediaPlayer.replaceCurrentResource` 播放特定資源。

例如：

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 確定要使用的媒體播放器 {#section_D844E386AF5848688D204DEE258ECEE6}

此示例過程說明了確定播放器技術的過程：

>[!TIP]
>
>進程可能因URL和環境而異。

1. 如果支援媒體源擴展，請使用它，但沒有已知限制。
1. 如果支援，請使用 `<video>` 直接標籤，而無MSE。
1. 確保您至少使用AdobeFlash Player版本23.0。
1. 如果找不到合適的回放技術， `replaceCurrentResource` 返回錯誤。

後續 `replaceCurrentResource` 呼叫相同 `MediaPlayer` 實例遵循同一進程。 這樣，您就可以使用 `MediaPlayer` 同一父代中的實例 `<DIV>` 您在 `MediaPlayerView` 已建立實例。

>[!TIP]
>
>SWF對象和 `<video>` 標籤嵌套在父代中 `<DIV>` 標籤。
