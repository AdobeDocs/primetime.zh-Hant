---
title: iOS自動播放
description: iOS自動播放
copied-description: true
exl-id: 591e8f74-63c3-4f74-9df4-024eb8aab646
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# iOS自動播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的卷API的實現允許在運行iOS版本10或更高版本的設備上自動播放內容。 iOS僅在音量靜音時允許自動播放。 當卷設定為零時，API將 `muted` 視頻標籤的屬性 `true`，否則 `muted` 屬性設定為 `false`。 的 `play` API啟動播放，而不需要任何用戶交互或用戶手勢。

要在iPhone上自動播放，請另外設定 `playsInline` 屬性 `video` 標籤 `true`。

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用 `playsInline` 屬性在不使用全屏模式的情況下啟動播放。
