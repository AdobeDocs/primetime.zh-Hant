---
description: 'null'
seo-description: 'null'
seo-title: 在iOS上自動播放
title: 在iOS上自動播放
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 在iOS上自動播放{#autoplay-on-ios}

AdobePSDK.MediaPlayer的大量API實作可讓執行iOS 10版或更新版本的裝置自動播放內容。 iOS僅允許在靜音時自動播放。 當卷設定為零時，API會將視頻標 `muted` 簽的屬性設定為 `true`，否則 `muted` 該屬性設定為 `false`。 API `play` 會啟動播放，而不需使用者互動或使用者手勢。

若是在iPhone上自動播放，請另 `playsInline` 將標籤的屬 `video` 性設為 `true`。

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>使用屬 `playsInline` 性可啟動未使用全螢幕模式的播放。

