---
title: Primetime 發行說明
description: Primetime 發行說明
copied-description: true
translation-type: tm+mt
source-git-commit: 944bfb0f3bd0050a9d2974a37f4fabddaaac8a93
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 26%

---


# Primetime 發行說明

歡迎使用Adobe Primetime發行說明。 左側導覽中列出的檔案可提供特定版本的資訊、系統需求、限制、已修正問題和已知問題。

## TVSDK 3.13 iOS中的增強功能和修正

本版次針對即時、VOD和FER串流提供DEMUXED &#39;HLS/CMAF&#39;（前滾、移轉和後滾）廣告支援。

如需其他修正和詳細資訊，請參閱「iOS適用的TVSDK發行說明」](../release-notes/tvsdk-3x-ios.md)[

## PTAI 21.2.2的增強功能和修正

該版本包括對HLS流中EXT-X-IMAGE-STREAM-INF流插入／同步的支援。 此功能是透過伺服器端組態來啟用的。 請連絡您的技術帳戶代表以啟用此功能。

## TVSDK 3.13 Android中的修正

此版本針對FireTV裝置上Widevine DRM串流凍結或顯示ABR開關黑色畫格的問題提供解決方法，這些裝置包括Fire TV第3代墜飾和Fire TV Cube第1代和第2代裝置。

若要解決此問題，請在開始播放之前，先針對指定的Fire TV裝置設定API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`。 預設值為false。

如需詳細資訊，請參閱[TVSDK for Android發行說明](../release-notes/tvsdk-3x-android.md)。

## TVSDK 3.12 iOS版本注意事項中的增強功能和修正

本版次著重於解決主要客戶問題。

如需[iOS](../release-notes/tvsdk-3x-ios.md)目前發行版本的詳細資訊，請參閱。

## 另請參閱

| 使用指南 | 說明 |
|--- |--- |
| [Primetime 程式設計說明](/help/programming/home.md) | 可讓您在 Android 裝置上使用 Java 和使用 iOS 裝置上使用 Objective-C 來學習開發應用程式和影片播放程式。 |
| [Primetime移轉與轉換說明](/help/migration-guides/home.md) | 說明從您現有的 Primetime TVSDK 套裝轉換及移轉至新一代套裝的程序。 |
| [參考實作](/help/android-reference-implementation/home.md) | 協助了解 TVSDK 並修改功能管理員，以自訂您的個人播放器。 |
| [Primetime API參考](/help/reference/api-references.md) | 提供有關 TVSDK 函數、資料結構和其他程式設計建構的詳細資訊。 |
| [Digital Rights Management](/help/digital-rights-management/home.md) | 協助您進一步瞭解Digital Rights Management(DRM)中的各種使用者案例 |
| [Primetime Ad Insertion 支援](/help/primetime-ad-insertion/home.md) | 說明如何透過在伺服器上插入以使用者為目標的動態廣告，從內容創造營收，並透過個人化廣告吸引對象。 |
| [封存](https://helpx.adobe.com/primetime/archives.html) | 下載已封存檔案的PDF。 |

## 有用的資源

* [瞭解Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [並行監視](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime驗證](https://tve.helpdocsonline.com/home)

* [Adobe PrimetimeDRM論壇](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime開發人員資源](https://www.adobe.com/devnet/primetime.html)
