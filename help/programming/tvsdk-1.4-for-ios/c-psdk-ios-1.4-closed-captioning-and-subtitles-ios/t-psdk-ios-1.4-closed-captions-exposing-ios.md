---
description: 若要讓您的使用者端播放器可以使用隱藏式字幕，您必須啟用它們。 使用者可以開啟或關閉隱藏式字幕，並選取格式。
title: 公開隱藏式字幕
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 公開隱藏式字幕 {#expose-closed-captions}

若要讓您的使用者端播放器可以使用隱藏式字幕，您必須啟用它們。 使用者可以開啟或關閉隱藏式字幕，並選取格式。

若要顯示隱藏式字幕：

1. 在 `PTMediaPlayer` 物件，設定 `closedCaptionDisplayEnabled` 屬性。

   如果使用者已啟用隱藏式字幕，此步驟會顯示文字。

   >[!NOTE]
   >
   >使用者端使用者可使用iOS協助工具設定來開啟或關閉隱藏式字幕，這些設定也提供格式選項。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 屬性已過時。 使用 `subtitlesOptions` 屬性 `PTMediaPlayerItem`. 另請參閱 [公開字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) 以使用隱藏式字幕。
