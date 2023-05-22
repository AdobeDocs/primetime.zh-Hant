---
description: 要使隱藏字幕對客戶端播放器可用，必須啟用它們。 用戶可以開啟或關閉隱藏字幕並選擇格式。
title: 公開隱藏的字幕
exl-id: 57168c6e-a958-4a89-b22b-0c9f1cab3a49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 公開隱藏的字幕 {#expose-closed-captions}

要使隱藏字幕對客戶端播放器可用，必須啟用它們。 用戶可以開啟或關閉隱藏字幕並選擇格式。

要公開隱藏字幕：

1. 在 `PTMediaPlayer` 對象，設定 `closedCaptionDisplayEnabled` 屬性。

   如果用戶已啟用隱藏字幕，則此步驟將顯示文本。

   >[!NOTE]
   >
   >客戶端用戶使用「iOS輔助功能設定」開啟或關閉關閉字幕，這些設定還提供了格式選項。

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` 不建議使用屬性。 使用 `subtitlesOptions` 物業 `PTMediaPlayerItem`。 請參閱 [曝光字幕](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) 以使用隱藏字幕。
