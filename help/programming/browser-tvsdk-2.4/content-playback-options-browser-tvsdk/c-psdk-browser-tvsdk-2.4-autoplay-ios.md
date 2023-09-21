---
title: 在iOS上自動播放
description: 在iOS上自動播放
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 在iOS上自動播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer音量API的實作可在執行iOS 10版或以上版本的裝置上自動播放內容。 iOS僅在音量靜音時允許自動播放。 當磁碟區設為0時，API會將 `muted` 要插入的視訊標籤屬性 `true`，否則 `muted` 屬性已設為 `false`. 此 `play` API會開始播放，不會發生任何使用者互動或使用者手勢。

若要在iPhone上自動播放，請另外設定 `playsInline` 的屬性 `video` 標籤至 `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用 `playsInline` 屬性會以非全熒幕模式啟動播放。
