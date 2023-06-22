---
description: 您可以使用Adobe Primetime廣告決策介面，在VOD和即時/線性內容中插入廣告。
title: 廣告需求
exl-id: b162e5b0-9f6c-46de-85de-97cec009a9b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 廣告逾時 {#ad-timeout}

## AV基礎需求 {#av-foundation-requirements}

若為VOD內容，播放清單彙整（涉及主要內容資訊清單載入、廣告解析和廣告資訊清單載入）應在35秒內完成。

如果是即時內容，每次更新播放清單時，播放清單拼接應在20秒內完成

**與AdResolution逾時相關的API**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

設定廣告中繼資料時，您可以透過設定PTAdMetadata：：adResolutionTimeout來設定adResolutionTimeout。

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

接著，請遵循以下章節： [Primetime廣告伺服器中繼資料](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**與AdManifest逾時相關的API**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

設定廣告中繼資料時，您可以透過設定PTAdMetadata：：adManifestTimeout來設定adManifestTimeout。


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

接著，請遵循以下章節： [Primetime廣告伺服器中繼資料](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
