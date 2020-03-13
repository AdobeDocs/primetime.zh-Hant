---
description: 若要讓用戶端播放器可使用隱藏字幕，您必須啟用隱藏字幕。 使用者可以開啟或關閉隱藏字幕，並選取格式。
seo-description: 若要讓用戶端播放器可使用隱藏字幕，您必須啟用隱藏字幕。 使用者可以開啟或關閉隱藏字幕，並選取格式。
seo-title: 公開隱藏字幕
title: 公開隱藏字幕
uuid: 209b34ca-f14e-499e-af5f-2d8c7b359ef8
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b

---


# 公開隱藏字幕 {#expose-closed-captions}

若要讓用戶端播放器可使用隱藏字幕，您必須啟用隱藏字幕。 使用者可以開啟或關閉隱藏字幕，並選取格式。

要顯示隱藏字幕：

1. 在對 `PTMediaPlayer` 像中，設定屬 `closedCaptionDisplayEnabled` 性。

   如果使用者已啟用隱藏字幕，此步驟會顯示文字。

   >[!NOTE]
   >
   >用戶端使用「iOS協助工具設定」來開啟或關閉關閉的字幕，這些設定也提供格式選項。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 屬性已過時。 使用 `subtitlesOptions` 屬性 `PTMediaPlayerItem`。 請參 [閱顯示字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) ，以使用隱藏字幕。