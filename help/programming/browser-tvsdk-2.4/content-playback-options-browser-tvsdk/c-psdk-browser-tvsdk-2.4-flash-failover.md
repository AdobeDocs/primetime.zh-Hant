---
description: 瀏覽器TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可以將其與其他Primetime元件整合。
title: Flash容錯移轉
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Flash容錯移轉 {#flash-failover}

瀏覽器TVSDK提供建立進階視訊播放器應用程式（您的Primetime播放器）的工具，您可以將其與其他Primetime元件整合。

使用平台的工具來建立播放器，並將其連線至瀏覽器TVSDK中的媒體播放器檢視，該檢視具有播放和管理視訊的方法。 例如，瀏覽器TVSDK提供播放和暫停方法。 您可以在平台上建立使用者介面按鈕，並設定呼叫這些瀏覽器TVSDK方法的按鈕。

## Flash遞補 {#section_92D3884A13A6431F9A9CC5C79715D888}

在瀏覽器TVSDK中，您的應用程式只會與 `Primetime.js` API。 基礎瀏覽器TVSDK實作會根據目前平台和要播放的媒體資源型別，決定要使用哪個播放器技術。

您必須呼叫，才會針對播放器技術做出決定 `MediaPlayer.replaceCurrentResource` 播放特定資源。

例如：

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## 決定要使用的媒體播放器 {#section_D844E386AF5848688D204DEE258ECEE6}

此範例程式說明決定播放器技術的程式：

>[!TIP]
>
>此程式可能會因URL和您的環境而異。

1. 如果支援Media Source Extensions，請使用它而沒有已知限制。
1. 如果支援，請使用 `<video>` 標籤而不使用MSE。
1. 確保您至少使用AdobeFlash Player23.0版。
1. 如果找不到合適的播放技術， `replaceCurrentResource` 傳回錯誤。

後續的 `replaceCurrentResource` 對相同專案呼叫 `MediaPlayer` 執行個體會遵循相同程式。 這可讓您使用相同的播放器來播放各種資源型別 `MediaPlayer` 相同父項中的執行個體 `<DIV>` 標籤之前指定的時間 `MediaPlayerView` 執行個體已建立。

>[!TIP]
>
>SWF物件與 `<video>` 標籤已巢狀內嵌於父項中 `<DIV>` 標籤之間。
