---
description: 若要讓您的使用者端播放器可以使用隱藏式字幕，您必須啟用它們。 使用者可以開啟或關閉隱藏式字幕，並選取格式。
title: 公開隱藏式字幕
exl-id: 6383a2b2-04e3-4fe1-a573-5e1f1ef486ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 公開隱藏式字幕 {#expose-closed-captions}

若要讓您的使用者端播放器可以使用隱藏式字幕，您必須啟用它們。 使用者可以開啟或關閉隱藏式字幕，並選取格式。

若要顯示隱藏式字幕，請執行下列動作：

1. 在 `PTMediaPlayer` 物件，設定 `closedCaptionDisplayEnabled` 屬性。

   如果使用者已啟用隱藏式字幕，此步驟會顯示文字。

   >[!NOTE]
   >
   >使用者端使用者可使用iOS協助工具設定來開啟或關閉隱藏式字幕，而這些設定也提供格式選項。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 屬性已過時。 使用 `subtitlesOptions` 屬性 `PTMediaPlayerItem`. 另請參閱 [公開字幕](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) 以使用隱藏式字幕。
