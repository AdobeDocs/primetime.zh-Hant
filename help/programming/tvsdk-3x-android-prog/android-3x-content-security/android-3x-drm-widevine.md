---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案來取代Adobe的整合解決方案。
title: Widevine DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Widevine DRM {#widevine-drm}

您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案來取代Adobe的整合解決方案。

請洽詢您的Adobe代表，以取得有關協力廠商DRM解決方案可用性的最新資訊。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以搭配HLS CMAF串流使用Android原生Widevine DRM。

>[!NOTE]
>
> Widevine CENC CTR Scheme需要最低版本4.4(API Level 19)。
>
> Widevine CBCS Scheme需要最低的Android 7.1版(API Level 25)。

## 設定許可證伺服器詳細資訊{#license-server-details}

在載入MediaPlayer資源前，請呼叫下列`com.adobe.mediacore.drm.DRMManager` API:

```java
public static void setProtectionData(
String drm,
String licenseServerURL,
Map<String, String> requestProperties)
```

### 參數{#arguments-license-server}

* `drm` -  `"com.widevine.alpha"` for Widevine。

* `licenseServerURL` -接收授權要求的Widevine授權伺服器URL。

* `requestProperties` -包含要包含在傳出授權請求中的額外標題。

例如，當使用Expressplay DRM封裝的內容時，請在播放前使用下列程式碼：

```java
DRMManager.setProtectionData(
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null);
```

## 提供自訂回呼{#custom-callback}

在載入MediaPlayer資源前，請呼叫下列`com.adobe.mediacore.drm.DRMManager` API。

```java
public static void setMediaDrmCallback(
MediaDrmCallback callback)
```

### 參數{#arguments-custom-callback}

* `callback` -自訂實作MediaDrmCallback，以取代預設值 `com.adobe.mediacore.drm.WidevineMediaDrmCallback`。

如需詳細資訊，請參閱[Android TVSDK 3.11 API檔案](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.11/index.html)。

## 擷取目前載入之MediaPlayer資源{#pssh-box-mediaplayer-resoource}的PSSH方塊

請呼叫下列`com.adobe.mediacore.drm.DRMManager` API，最好是在自訂回呼實作中。

```java
public static byte[] getPSSH()
```

API返回與載入的Widevine媒體資源關聯的「保護系統特定報頭框」。

有效方塊可在較短期間內使用（在DRM實例建立和鍵的載入之間）。 `MediaDrmCallback callback executeKeyRequest()` 可用來自訂擷取授權金鑰。

>[!NOTE]
>
> `getPSSH()` API僅支援單一播放器例項。多個播放器或「立即啟動」功能應依序初始化，以接收正確的方塊。
