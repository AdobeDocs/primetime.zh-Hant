---
title: Primetime 發行說明
description: Primetime 發行說明
copied-description: true
exl-id: 29087a3e-f16e-4510-8d3a-ed2229700899
source-git-commit: 97a192ed1d0ddc034f72a836a70293acfcca9881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 29%

---

# Primetime 發行說明

歡迎使用Adobe Primetime發行說明。 左側導覽中列出的檔案提供版本專屬資訊、系統需求、限制、已修正問題和已知問題。

## PTAI 21.8.1中的增強功能和修正

此版本包含對DASH即時/線性資料流的支援。

如需其他修正和詳細資訊，請參閱[Ad Insertion發行說明](/help/release-notes/ptai-21x-release-notes.md)

## TVSDK 3.13 iOS中的增強功能和修正

此版本推出對即時、VOD和FER資料流的DEMUXED &#39;HLS/CMAF&#39;（前段、midroll和postroll）廣告的支援。

如需其他修正和詳細資訊，請參閱iOS適用的TVSDK發行說明](../release-notes/tvsdk-3x-ios.md)[

## TVSDK 3.13 Android中的修正

此版本針對FireTV裝置（包括Fire TV第3代吊墜和Fire TV Cube第1和第2代裝置）上的ABR開關上的Widevine DRM資料流凍結或顯示黑格的問題提供了解決方法。

若要解決此問題，請在開始播放之前，為指定的Fire TV裝置設定API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`。 預設值為false。

如需詳細資訊，請參閱Android適用的[ TVSDK發行說明](../release-notes/tvsdk-3x-android.md) 。

## 另請參閱

| 使用手冊 | 說明 |
|--- |--- |
| [Primetime 程式設計說明](/help/programming/home.md) | 可讓您在 Android 裝置上使用 Java 和使用 iOS 裝置上使用 Objective-C 來學習開發應用程式和影片播放程式。 |
| [Primetime移轉與轉換說明](/help/migration-guides/home.md) | 說明從您現有的 Primetime TVSDK 套裝轉換及移轉至新一代套裝的程序。 |
| [參考實作](/help/android-reference-implementation/home.md) | 協助了解 TVSDK 並修改功能管理員，以自訂您的個人播放器。 |
| [Primetime API參考](/help/reference/api-references.md) | 提供有關 TVSDK 函數、資料結構和其他程式設計建構的詳細資訊。 |
| [Digital Rights Management](/help/digital-rights-management/home.md) | 協助您進一步了解Digital Rights Management(DRM)中的各種使用者案例 |
| [Primetime Ad Insertion 支援](/help/primetime-ad-insertion/home.md) | 說明如何透過在伺服器上插入以使用者為目標的動態廣告，從內容創造營收，並透過個人化廣告吸引對象。 |
| [封存](https://helpx.adobe.com/primetime/archives.html) | 下載已封存檔案的PDF。 |

## 實用資源

* [了解Adobe Primetime](https://www.adobe.com/in/marketing/primetime.html)

* [併發監控](https://tve.helpdocsonline.com/concurrency-monitoring-introduction)

* [Primetime驗證](https://tve.helpdocsonline.com/home)

* [Adobe Primetime DRM論壇](https://forums.adobe.com/community/adobe_access)

* [Adobe Primetime開發人員資源](https://www.adobe.com/devnet/primetime.html)
