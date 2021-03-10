---
description: 您可以使用Adobe Primetime廣告決策介面，在VOD和即時／線性內容中插入廣告。
title: 廣告需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 廣告逾時{#ad-timeout}

## AV Foundation要求{#av-foundation-requirements}

如果是VOD內容，則播放清單拼接（包括主要內容資訊清單載入、廣告解析度和廣告資訊清單載入）應在35秒內完成。

如果是即時內容，每次更新播放清單時，應在20秒內完成播放清單連結

**與AdResolution逾時相關的API**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

您可以在設定廣告中繼資料時，設定PTAdMetadata::adResolutionTimeout，以設定adResolutionTimeout。

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

之後，請依照以下章節：[Primetime廣告伺服器中繼資料](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)。

**與AdManifest逾時相關的API**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

您可以在設定廣告中繼資料時，設定PTAdMetadata::adManifestTimeout，以設定adManifestTimeout。


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

之後，請依照以下章節：[Primetime廣告伺服器中繼資料](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md)。
