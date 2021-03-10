---
description: 若要讓用戶端播放器可使用隱藏字幕，您必須啟用隱藏字幕。 使用者可以開啟或關閉隱藏字幕，並選取格式。
title: 公開隱藏字幕
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 公開隱藏隱藏字幕{#expose-closed-captions}

若要讓用戶端播放器可使用隱藏字幕，您必須啟用隱藏字幕。 使用者可以開啟或關閉隱藏字幕，並選取格式。

要顯示隱藏字幕：

1. 在`PTMediaPlayer`物件中，設定`closedCaptionDisplayEnabled`屬性。

   如果使用者已啟用隱藏字幕，此步驟會顯示文字。

   >[!NOTE]
   >
   >用戶端使用「iOS協助工具設定」來開啟或關閉關閉的字幕，這些設定也提供格式選項。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 屬性已過時。使用`PTMediaPlayerItem`的`subtitlesOptions`屬性。 請參閱[公開字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md)以使用隱藏字幕。