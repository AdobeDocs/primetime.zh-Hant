---
title: 在iOS上自動播放
description: 在iOS上自動播放
copied-description: true
exl-id: 591e8f74-63c3-4f74-9df4-024eb8aab646
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# 在iOS上自動播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的磁碟區API實作可在執行iOS 10版或更新版本的裝置上自動播放內容。 iOS僅在音量靜音時允許自動播放。 當磁碟區設為0時，API會將 `muted` 的視訊標籤屬性 `true`，否則會 `muted` 屬性已設定為 `false`. 此 `play` API會啟動播放，而不需要任何使用者互動或使用者手勢。

若要在iPhone上自動播放，請另外設定 `playsInline` 的屬性 `video` 標籤至 `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用 `playsInline` 屬性會在沒有全熒幕模式的情況下開始播放。
