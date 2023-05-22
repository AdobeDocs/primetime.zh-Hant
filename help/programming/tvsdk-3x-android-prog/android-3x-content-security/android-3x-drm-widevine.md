---
description: 您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合解決方案的替代方案。
title: 維德文DRM
exl-id: 44ab032e-e665-4b63-a08b-54e862894987
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 維德文DRM {#widevine-drm}

您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合解決方案的替代方案。

有關第三方DRM解決方案的可用性的最新資訊，請與Adobe代表聯繫。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以將Android本機Widevine DRM與HLS CMAF流一起使用。

>[!NOTE]
>
> Widevine CENC CTR方案要求Android 4.4版(API Level 19)最低。
>
> Widevine CBCS方案要求Android 7.1版(API Level 25)的最低要求。

## 設定許可證伺服器詳細資訊 {#license-server-details}

呼叫以下 `com.adobe.mediacore.drm.DRMManager` 載入MediaPlayer資源之前的API:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 參數 {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` 維迪文的。

* `licenseServerURL`  — 接收許可證請求的WideVine許可證伺服器的URL。

* `requestProperties`  — 包含要包括在傳出許可證請求中的額外標頭。

例如，在使用為Expressplay DRM打包的內容時，在播放前使用以下代碼：

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## 提供自定義回調 {#custom-callback}

呼叫以下 `com.adobe.mediacore.drm.DRMManager` 載入MediaPlayer資源之前的API。

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 參數 {#arguments-custom-callback}

* `callback`  — 自定義MediaDrmCallback實現，以代替預設 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`。

有關詳細資訊，請參閱 [Android TVSDK 3.11 API文檔](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html)。

## 獲取當前載入的MediaPlayer資源的PSSH框 {#pssh-box-mediaplayer-resoource}

呼叫以下 `com.adobe.mediacore.drm.DRMManager` API，最好在自定義回調實現中。

```java
public static byte[] getPSSH()
```

API返回與載入的WideVine媒體資源關聯的保護系統特定報頭框。

有效框的持續時間很短（在DRM實例建立和鍵的載入之間）。 `MediaDrmCallback callback executeKeyRequest()` 可以使用它自定義獲取許可證密鑰。

>[!NOTE]
>
> `getPSSH()` 僅單播放器實例支援API。 多個播放器或「即時開啟」功能應按順序初始化以接收正確的框。
