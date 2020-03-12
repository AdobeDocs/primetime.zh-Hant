---
description: 瀏覽器TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可將其與其他Primetime元件整合。
seo-description: 瀏覽器TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可將其與其他Primetime元件整合。
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Flash容錯功能 {#flash-failover}

瀏覽器TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可將其與其他Primetime元件整合。

使用您平台的工具來建立播放器，並將它連接至瀏覽器TVSDK中的媒體播放器檢視，該檢視有播放和管理視訊的方法。 例如，瀏覽器TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定按鈕來呼叫這些瀏覽器TVSDK方法。

## Flash備援 {#section_92D3884A13A6431F9A9CC5C79715D888}

在瀏覽器TVSDK中，您的應用程式僅與 `Primetime.js` API互動。 基礎的瀏覽器TVSDK實作會根據目前的平台和要播放的媒體資源類型，決定要使用的播放器技術。

在您呼叫播放特定資源之前，才會決 `MediaPlayer.replaceCurrentResource` 定播放器技術。

例如：

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 確定要使用的媒體播放器 {#section_D844E386AF5848688D204DEE258ECEE6}

此範例程式說明決定播放器技術的程式：

>[!TIP]
>
>程式會視URL和您的環境而有所不同。

1. 如果支援「媒體來源擴充功能」，請使用它，但不受已知限制。
1. 如果支援，請直接使 `<video>` 用標籤，而不需MSE。
1. 請確定您至少使用Adobe Flash Player 23.0版。
1. 如果找不到合適的播放技術， `replaceCurrentResource` 則返回錯誤。

對同一 `replaceCurrentResource` 實例的後續調用 `MediaPlayer` 遵循相同的流程。 這可讓您在建立執行個體時所指定的相同父 `MediaPlayer` 代標籤中，使用 `<DIV>` 相同的執行個體來播放 `MediaPlayerView` 各種資源類型。

>[!TIP]
>
>SWF物件和標 `<video>` 簽會巢狀內嵌在父標籤 `<DIV>` 中。

