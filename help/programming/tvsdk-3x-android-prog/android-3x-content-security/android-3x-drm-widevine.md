---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您可以使用協力廠商DRM解決方案作為Adobe整合解決方案的替代方案。
title: Widevine DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您可以使用協力廠商DRM解決方案作為Adobe整合解決方案的替代方案。

請連絡您的Adobe代表，以取得有關協力廠商DRM解決方案可用性的最新資訊。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以搭配HLS CMAF資料流使用Android原生Widevine DRM。

>[!NOTE]
>
> Widevine CENC CTR Scheme至少需要Android 4.4版(API Level 19)。
>
> Widevine CBCS Scheme至少需要Android 7.1版(API Level 25)。

## 設定授權伺服器詳細資料 {#license-server-details}

呼叫下列專案 `com.adobe.mediacore.drm.DRMManager` 載入MediaPlayer資源前的API：

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 引數 {#arguments-license-server}

* `drm` - `"com.widevine.alpha"` 給Widevine。

* `licenseServerURL`  — 接收授權要求的Widevine授權伺服器URL。

* `requestProperties`  — 包含要包含在傳出授權請求中的額外標頭。

例如，使用封裝為Expressplay DRM的內容時，在播放之前請使用下列程式碼：

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## 提供自訂回撥 {#custom-callback}

呼叫下列專案 `com.adobe.mediacore.drm.DRMManager` 載入MediaPlayer資源之前的API。

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 引數 {#arguments-custom-callback}

* `callback`  — 自訂的MediaDrmCallback實作，以取代預設值 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`.

如需詳細資訊，請參閱 [Android TVSDK 3.11 API檔案](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html).

## 擷取目前載入之MediaPlayer資源的PSSH方塊 {#pssh-box-mediaplayer-resoource}

呼叫下列專案 `com.adobe.mediacore.drm.DRMManager` API，最好在自訂回呼實施中進行。

```java
public static byte[] getPSSH()
```

API會傳回與已載入Widevine媒體資源相關聯的Protection System Specific標頭方塊。

有效方塊可用於較短的持續時間（在DRM例證建立和載入金鑰之間）。 `MediaDrmCallback callback executeKeyRequest()` 可使用它來自訂擷取授權金鑰。

>[!NOTE]
>
> `getPSSH()` API僅支援單一播放器例項。 多個播放器或「立即開啟」功能應依序初始化，才能收到正確的方塊。
