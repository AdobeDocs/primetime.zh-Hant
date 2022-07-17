---
title: 瀏覽器TVSDK 2.4發行說明
description: 瀏覽器TVSDK 2.4發行說明描述了瀏覽器TVSDK 2.4中新的、受支援的和不受支援的功能以及已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# 瀏覽器TVSDK 2.4發行說明 {#browser-tvsdk-release-notes}

瀏覽器TVSDK 2.4發行說明描述了瀏覽器TVSDK 2.4中新的、受支援的和不受支援的功能以及已知問題。

## 導言 {#introduction}

瀏覽器TVSDK是一個工具包，允許您向基於瀏覽器的視頻播放器應用程式添加高級視頻播放功能、內容保護和廣告。

瀏覽器TVSDK 2.4提供JavaScript API來構建基於瀏覽器的視頻應用程式，並包括以下模式的回放支援：

* 僅HTML5
* HTML5，帶自動快閃記憶體回退
* Flash始終

本版本包括以下資訊：

· [瀏覽器TVSDK API文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

· [瀏覽器TVSDK寫程式指南](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf)。

· [《 TVSDK for 1.4 DHLS to Browser TVSDK 2.4遷移指南》](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

· [從瀏覽器TVSDK 2.4.6轉換到2.4.7版](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html)。

·參考實施，包括在構建中。

>[!NOTE]
>
>*有關此版本的安全注意事項的完整清單，請參閱安全注意事項。

## 新增和支援的功能 {#what-s-new-and-supported-features}

此版本的瀏覽器TVSDK提供了可用於增強視頻應用程式的新功能。

**2.4.12更新(Build 204)中的新增功能**

以下增補內容可作為Browser TVSDK 2.4.12更新(Build 204)的一部分：

* AdobePSDK.MediaPlayer的卷API的實現被更改為允許在播放靜音時在iOS上自動播放。

·新的API, `auditudeSettings.ignoreVPAIDAds`，以允許忽略從Auditude伺服器接收的VPAID廣告。 API不適用於Flash回退。

**2.4.11版**

以下增強和增補功能是Browser TVSDK 2.4.11版的一部分：

· MSE和Flash回退模式支援HLS Live段故障切換。

·支援 `AuditudeSettings.creativeRepackagingDomain` API現在也可用於MSE。 以前只支援Flash回退模式。

·此版本包含針對關鍵客戶問題的修復。 請參閱 *已修復的問題* 清單。

**2.4.10版**

以下增強和增補功能是Browser TVSDK 2.4.10版的一部分：

· TVSDK提供enableLogging()以啟用或禁用日誌記錄。 請參閱 [API文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)的子菜單。

·使用Adobe Analytics時，TVSDK不再支援預設章節。 使用應用程式定義和管理章節。

·此版本包含針對關鍵客戶問題的修復。 請參閱*問題已修復*清單。

**2.4.9版**

以下增強和增補功能是Browser TVSDK 2.4.9版的一部分：

·支援具有時間不連續但沒有不連續標籤的HLS視頻點播和即時流。

· HLS VOD和Live流的Safari視頻標籤支援ID3 v2.4.0幀。

·安全Ad載入實現可確保基於API配置將ad伺服器調用升級到安全HTTP。 有關詳細資訊，請參見AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration類。 在Flash回退模式中不支援此功能。

·與VAST 3.0響應相關的廣告ID資訊和擴展資訊現在由TVSDK提供給應用程式，並可用於實現Moat整合以進行廣告測量。 有關詳細資訊，請參閱AdobePSDK.NetworkAdInfo API。 在Flash回退模式中不支援此操作。

· AdobePSDK.ForceHttpsConfiguration類不再可用。 成功者

AdobePSDK.ForceHttpsAdConfiguration類。

·現在可以使用新的API AdobePSDK.optimizeFlashCalls來優化調用，以改進Flash回退模式下的HLS回放體驗。 預設情況下，此選項為禁用狀態。

**2.4.8更新(Build 6002)中的新增功能**

此更新包含針對關鍵客戶問題的修復。 請參閱 *已修復問題*&#x200B;的雙曲餘切值。

**2.4.8版**

以下增強和增補功能是Browser TVSDK 2.4.8版的一部分：

· SDK現在與Chrome EME相容，從Chrome v58開始提供的最佳做法更改。 有關詳細資訊，請參閱 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI框架現在支援Flash、僅廣告和目標資訊工作流上的HLS訪問DRM。

·將setDRMAuthenticateData API添加到UI框架。 要播放使用Adobe訪問DRM保護的流，請調用此API。 或者，可以在播放器中指定drmAuthenticateData屬性。 請參閱 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)的雙曲餘切值。

**2.4.7版**

以下功能是2.4.7版中的新增功能：

·在UI框架中添加UI配置器

可以通過以下方式之一配置播放器：

·使用JSON對象

·使用API

為幫助生成JSON對象，Browser TVSDK提供了**UI配置器**工具。

在此工具中，您可以選擇各種設定，按一下**Test配置**驗證設定，然後按一下**下載配置**下載設定。 下載檔案後，可以將此檔案的內容作為JSON對象傳遞給ptp.videoPlayer API。

·將MediaPlayerItemConfig API添加到UI框架

可通過MediaPlayerItemConfig配置各種功能，包括advertisingMetadata、advertisingFactory、adSigningMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscribeTags、thumbnailScruber、bilingMetricsConfig。 有關詳細資訊，請參閱 [瀏覽器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* [文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

在UI框架中，通過播放器配置傳遞網路配置的方式已被修改。

**2.4.6版**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**2.4.7版**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* 在UI框架中支援DRM和分析工作流

可以通過UI框架啟用DRM配置和分析跟蹤。

* 增加 `AdobePSDK.embedSWFinFullScreenDiv` API

此新API為播放器應用程式提供了選擇可嵌入FlashFallback.swf檔案的div的靈活性。

* 已更換 `getVersion`API來自 `AdobePSDK.MediaPlayer` 類 `AdobePSDK.Version` 類，用於TVSDK版本相關資訊。 有關詳細資訊，請參閱 `AdobePSDK.Version` API [這裡](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html)。

**2.4.6版**

以下功能是2.4.6版中的新增功能：

* **瀏覽支援**

瀏覽器化允許您在瀏覽器中使用node.js樣式模組。 可以定義依賴關係，並瀏覽將所有內容捆綁到一個JavaScript檔案中。

* **計費**

借助計費，瀏覽器TVSDK可以收集玩家使用度量，對黃金時段客戶進行計費。

>[!NOTE]
>
>已在2.4.6版中刪除Enum PSDKErrorCode中棄用的枚舉MediaPlayer.Events和棄用的常數。有關詳細資訊，請參見 [從瀏覽器TVSDK 2.4.5轉換到2.4.6版](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html)。

**2.4.5版**

以下功能是2.4.5版中的新增功能：

* **完整事件重放和廣告**

   HLS全事件重播(FER)流現在支援廣告解析度和廣告行為。 要啟用此支援，請將ad信令模式設定為 `MANIFEST_CUES` 建立 `MediaPlayerItemConfig` 的雙曲餘切值。

* **MediaplayerView ScalePolicy支援**

   應用程式開發人員現在可以使用MediaplayerView scalePolicy屬性為視圖指定不同的scalePolicy。

* **變形內容支援**

   現在，使用MSE和Flash回放時支援變形內容回放。

* **選擇性應用`withCredentials`**

當 `withCredentials` 設定為true, `Access-Control-Allow-Origin` 標頭不能設定為通配符。 根據伺服器的響應，瀏覽器TVSDK將有選擇地設定 `withCredentials` 屬性。 有關此支援的詳細資訊，請參見 [瀏覽器TVSDK API文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

**2.4.4版**

以下功能是2.4.4版中的新增功能：

* **Chromecast示例應用**

本版本為發送方和接收方應用提供支援，該應用演示了通過客戶端和插入播放DASH VOD流和DASH Widevine流。

* **高級故障切換支援**

此版本支援HLS VOD流的高級故障切換使用情形（段和伺服器故障切換）。

**2.4.3版**

以下功能是2.4.3版中的新增功能：

* **DASH VOD的自定義標籤**

   內聯自定義標籤（事件）可以訂閱並作為TimedMetadata對象接收。

* **播放沒有副檔名的流**

   現在支援不擴展的HLS和DASH流。 對於清單檔案，在載入資源時需要指定resourceType。 對於段和VTT檔案，「內容類型」響應頭用於確定內容類型。

**2.4.2版**

以下功能是2.4.2版中的新增功能：

* **API奇偶校驗**

有關API奇偶校驗的完整清單，請參見 [《 TVSDK for 1.4 DHLS to Browser TVSDK 2.4遷移指南》](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

* **示例 — AES支援**

   此版本增加了對MSE和Flash回退上Sample-AES加密內容回放的支援。 GoogleChrome上通過安全原點承載AES內容的要求已經取消。

* **支援AAC容器**

   現在支援播放副檔名為.aac的檔案。 這可以是僅音頻流或備用音頻。

   >[!NOTE]
   >
   >AC3和增強的AC3編解碼器尚不受支援。

* **標籤化流播放**

通過內容分發網路(CDN)傳送的HLS流有時可以使用清單和段請求上的驗證令牌進行驗證，並且這些令牌可以作為URL參數或作為cookie標頭提供。 現在支援此類流的回放。

**2.4.1版**

以下功能是2.4.1版中的新增功能：

* **UI框架**

此框架旨在加快基於JavaScript的視頻播放器應用程式的UI開發，它包含API，用於包括基本控制項，如播放/暫停和音量，以及用於輕鬆添加或刪除諸如擦洗欄狀態和隱藏字幕設定的元素。 您可以指定與控制項關聯的行為、建立自定義控制項和使播放器UI外觀。 這都是通過框架實現的，不需要直接操作DOM結構。

* **HLS即時流回放增強功能**

此釋放支援由廣告插入引起的不連續。 它使用EXT-PROGRAM-DATE-TIME標籤，後跟EXT-MEDIA-SEQUENCE標籤，跨自適應比特率配置檔案進行同步，以便平滑回放。

* **VPAID 2.0支援**

視頻播放器廣告服務介面定義(VPAID)2.0版為用戶提供了豐富的媒體體驗，使出版商能夠更好地瞄準廣告，跟蹤廣告印象，並將視頻內容貨幣化。 本版本支援用於視頻點播(VOD)內容的線性JavaScript VPAID廣告。

* **自定義HLS標籤**

媒體流可以以播放清單/清單檔案中的標籤形式攜帶附加元資料。 瀏覽器TVSDK允許您指定和訂閱附加標籤，並在清單中出現這些標籤時通知您。

* **播放器時間線上顯示的廣告標籤**

此版本支援在VOD和Live內容的播放器時間軸上顯示廣告標籤。 您可以在參考播放器中看到此行為。

**在2.4中支援**

2.4版中提供了以下功能：

* **MP3音頻播放**

   此版本支援在具有媒體源擴展(MSE)和Safari視頻標籤的瀏覽器上播放MP3音頻。

* **MP4視頻播放**

   支援以下功能：

   * 單流播放
   * 具有廣告行為和跟蹤的預卷和後卷MP4廣告
   * 具有廣告行為和跟蹤的卷前和卷後HLS廣告
   * 具有廣告行為和跟蹤的預卷和後卷DASH廣告

## 支援的平台 {#supported-platforms}

瀏覽器TVSDK對需要運行的平台和軟體的級別有特定要求。 支援以下平台和軟體級別：

### 台式機配置 {#desktop-configurations}

* MicrosoftWindows 7:

   * Internet Explorer 11+
   * 鉻33+
   * 火狐38+

* MicrosoftWindows 8.1

   * Internet Explorer 11+
   * 鉻33+
   * 火狐38+

* MicrosoftWindows 10

   * 邊緣+

* AppleOS X

   * Safari 9+
   * 鉻33+
   * 火狐38+

### 移動Web配置 {#mobile-web-configurations}

* Android 4.4

   * 本機瀏覽器
   * 鉻33+

* Android 5.0

   * 本機瀏覽器
   * 鉻33+

* Android 6.0

   * ·鉻33+

* AppleiOS9

   * Safari 9+
   * 鉻33+

* AppleiOS10

   * Safari 9+
   * 鉻33+

**GoogleChromecast(第二代；僅適用於短划線回放)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>技術</strong> </p> </td> 
   <td><p><strong>瀏覽器TVSDK視頻標籤</strong><sup>1</sup></p> </td> 
   <td><p><strong>瀏覽器TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>預設技術</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>視頻標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>安卓</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>均方誤差</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple野生動物園8</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>視頻標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google鉻</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>均方誤差</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>均方誤差<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS，達什</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>均方誤差</p> </td> 
  </tr> 
 </tbody> 
</table>

## 特徵矩陣 {#feature-matrix}

以下是此版本支援的和不受支援的功能的清單：

* *MP3音頻功能 — 核心播放*
* *MP4視頻功能 — 核心播放*
* *MP4視頻功能 — 核心Ad Insertion*

>[!NOTE]
>
>*在下面的特徵矩陣表中，「Y」表示當前版本支援該特徵。*

### MP3音頻功能 {#mp-audio-features}

**表1:核心播放{#table-core-playback}**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3視頻點播 | 常規播放（播放、暫停、查找） | 不支援 | Y | Y |

1瀏覽器TVSDK視頻標籤不支援流式處理和DRM。 在所有瀏覽器中，編解碼器和容器支援不同。

2 Firefox預設為41版或更低版本的Flash Player。

### MP4音頻功能 {#mp-audio-features-1}

**表2:核心播放**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4視頻點播 | 常規播放（播放、暫停、查找） | 不支援 | Y | Y |

**表3:核心Ad Insertion**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4視頻點播 | 預卷(MP4) | 不支援 | Y | Y |
| Ad Insertion | MP4視頻點播 | 後輥(MP4) | 不支援 | Y | Y |

有關HLS或DASH功能支援的詳細資訊，請參閱下文。

## HLS特徵矩陣 {#hls-feature-matrix}

下面是瀏覽器TVSDK中HLS功能的功能清單。

* *HLS核心播放*
* *HLS高級回放功能*
* *HLS內容保護功能*
* *HLS核心和插入功能*
* *HLS高級和插入功能*
* *HLS整合*

>[!NOTE]
>
>*在下面的特徵矩陣表中，「Y」表示當前版本支援該特徵。*

### HLS功能 {#hls-features}

支援以下功能：

**表4:HLS核心播放**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>一般播放（播放、暫停、查找）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER視頻點播</p> </td> 
   <td><p>常規播放（播放、暫停和查找）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自適應比特率</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>僅VOD</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>清單故障轉移</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>高級故障切換</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>有限的QoS支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>支援Cookie標頭</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定緩衝區控制參數</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定自適應</p> <p>比特率控制</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自定義標籤</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>延遲綁定音頻</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302重定向</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
 </tbody> 
</table>

**表5:HLS高級回放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>偏移處回放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>僅音頻播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>特技遊戲</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>平滑特技遊戲</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3分析</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>不連續標籤支援</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>標籤化流</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>計費</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表6:HLS內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>樣本 — AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe訪問</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>公平遊戲</p> </td> 
  </tr> 
 </tbody> 
</table>

**表7:HLS核心和插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預軋(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>中間輥(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>輥後(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER視頻點播</p> </td> 
   <td><p>廣告解析度和行為</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預設廣告策略</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>廣2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>創意重新打包（MP4到HLS）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表8:HLS高級和插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>僅廣告</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>目標參數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自定義參數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自定義廣告策略</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>懶惰載入</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>夥伴廣告、橫幅廣告、可點擊廣告</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**表9:HLS整合{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:薩法里，iOS</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>整合</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe AnalyticsVHL整合</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## DASH特徵矩陣 {#dash-feature-matrix}

下面是瀏覽器TVSDK中DASH功能的功能矩陣。

· *DASH核心播放功能*

· *DASH高級回放功能*

· *DASH內容保護功能*

· *DASH核心和插入功能*

· *DASH高級廣告插入功能*

· *DASH整合*

>[!NOTE]
>
>在下面的特徵矩陣表中， Y表示在當前版本中支援該特徵。

### DASH功能 {#dash-features}

支援以下功能：

**表10:DASH核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>一般播放（播放、暫停、查找）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER視頻點播</p> </td> 
   <td><p>常規播放（播放、暫停和查找）</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自適應比特率</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>故障轉移</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>支援Cookie標頭</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定緩衝區控制參數</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定自適應比特率控制</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自定義標籤(EventStream)</p> </td> 
   <td><p>僅VOD（內聯）</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>後期綁定音頻</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302重定向</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**表11:DASH高級回放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>偏移處回放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>僅音頻播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>戲法</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>平滑特技遊戲</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3分析</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>多期支助</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>標籤化流</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>計費</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表12:DASH內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>樣本 — AES</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Chrome、Firefox 47及更高版本和Chromecast上的Widevine</p> <p>·在Windows 8.1和Edge上的Internet Explorer上播放PlayReady</p> <p>·用於Windows Firefox的黃金時段DRM（僅視頻）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13:DASH核心和插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預卷(MP4/DASH)</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>中間輥(DASH)</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>後滾(MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER視頻點播</p> </td> 
   <td><p>廣告解析度和行為</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預設廣告策略</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>廣2.0/3.0</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>創意重新打包（MP4到DASH）</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14:DASH高級廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>僅廣告</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>目標參數</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>自定義參數</p> </td> 
   <td><p>僅VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自定義廣告策略</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>懶惰載入</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>伴侶廣告、橫幅廣告、可點擊廣告</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>視頻點播</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
 </tbody> 
</table>

**表15:DASH整合**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>整合</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe AnalyticsVHL整合</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 已修復的問題 {#issues-fixed}

**在2.4.12更新(Build 204)中修復的問題**

以下問題已在瀏覽器TVSDK 2.4.12版更新(Build 204)中解決：

· **21647** — 當音頻靜音時，TVSDK應允許在iOS設備上自動播放視頻。

· **21465** — 播放DRM保護的DASH流後，在播放DASH Live流時收到錯誤密鑰系統訪問被拒絕。

· **21442** — 在用用戶手勢播放預播廣告後，啟用iOSWeb上的內容自動播放。

· **21240** — 提供的API用於過濾從Auditude/VMAP解析的VPAID廣告。

**2.4.11版中修復的問題**

以下問題已在瀏覽器TVSDK 2.4.11版中解決：

**核心播放功能：**

· **19192**:TVSDK現在實現TextFormat:bottomInset和TextFormat:safeArea。 由於這些增強功能，如果控制欄顯示在螢幕上，則可以重新定位隱藏字幕。

· **21009**:如果在出現新的字幕之前尋求跨越不連續性，則隱藏字幕會一直保留在螢幕上。

· **21141**:由於段追加期間存在競爭條件，返回尋道被拒絕。

· **21142**:使播放器處於INITIALIZED狀態時可用可查找的播放範圍。 由於這些更改，現在支援在位啟動會話。

· **21363**:在DASH流的廣告插入後，608/708隱藏字幕將失去同步。

**廣告插入功能：**

· **21179**:現在，通過正確設定ad.primaryAsset.adParameters屬性，可解決與VOD內容相關的中間卷問題（長暫停、黑幀）。

· **21257**:如果MP4不是有效的MIME類型，並且啟用了創意重新打包功能，則選擇具有最高比特率的MP4檔案進行轉碼。

· **21361**:TVSDK現在將廣告系統和創意ID作為查詢參數在創意打包請求中傳遞，以支援其他規範化規則。

**2.4.10版中修復的問題**

以下問題已在瀏覽器TVSDK 2.4.10版中解決：

**核心播放功能：**

· **21060**:HLS流包含中斷且ISO BMFF框運行到流末尾時引發的編解碼器錯誤無效。

· **21045**:在播放清單中的第一個視頻播放完成後，自動播放在iOS上不工作。

· **20975**:幀速率由Chrome瀏覽器上的QoS提供商以NaN的形式返回。

· **20823**:遇到沒有資料的段時引發不支援的編解碼器錯誤。

· **20769**:SDK現在以當前的尋道位速率開始，而不是基於ABR策略立即切換。

· **20031**:在IE11(Windows 8.1)上處於縱向模式時，視頻螢幕會變小。 內容保護功能：

· **19316**:跳過在HLS AES-128流中解密失敗的段。

**2.4.9版中修復的問題**

以下問題已在瀏覽器TVSDK 2.4.9版中解決：

**核心播放功能：**

· **13407**:如果Firefox在播放期間停止發送「ontimeupdate」事件，則DASH流可能會停止。

· **16380**:在通過MSE對具有不匹配起始時間的段進行混合音頻視頻內容回放期間，表示之間的音頻同步錯誤在ABR開關上累積，最終導致錯誤(鉻問題#663686)。

· **17985**:在Firefox瀏覽器上播放特定ISO-BMFF流時，播放會被卡住(Firefox問題#1342913)。 自Firefox v53以來已修復此問題。

· **19141**:未捕獲（在承諾中）ReferenceError:寬度未定義。

· **18997、19299**:段邊界處的視頻閃爍問題。 這是因為SDK未正確計算上一個示例的合成時間偏移。

· **19780**:在Firefox v53上，HLS內容和HLS Ad不會啟動播放(Firefox問題#354653)。

· **20046**:程式日期時間在作為定時元資料對象接收時作為鍵而不是值接收。

· **20047**:useDefaultResizeHandler引發Flash回退錯誤。

· **20179**:Flash回退不使用Flash Playerv25.0.0.171。

· **20293**:Firefox停止緩衝某些HLS流的資料，導致資料停止。

· **20626**:Player在Chrome上拋出媒體解碼錯誤，因為對持續時間為零的視頻樣本處理不正確。

· **20078**:瀏覽器錯誤「QuotaExceeded」上的播放停止。

· **18639**:在HLS Live stream 608 CC文本中，有時顯示為拼寫錯誤。

· **20028**:ClosedCaptions大小參數不更改字型大小。

· **20613**:隱藏的字幕框相互重疊，使其難以辨認。

**核心Ad Insertion(CSAI)功能：**

· **20043**:使用多個廣告和第三方重定向缺少廣告印象和廣告跟蹤呼叫。

· **20044**:使用創造性重新包裝時，廣告片段中的所有廣告都需要成功地重新包裝，否則廣告片段將被完全丟棄。

· **20097**:跳過廣告播放，主內容立即恢復，而不是等待超時20秒（如果廣告清單不可用）。

**2.4.8版更新(Build 6002)中修復的問題**

以下問題已在瀏覽器TVSDK 2.4.8版更新(Build 6002)中解決：

· **14126:** 由於MSE源緩衝區中的內部間隙，Firefox(問題#1316024)上的回放可能會停止。 嘗試查找以恢復播放

· **19608:** 修復以從Auditude VMAP響應中恢復時間偏移值。

· **19635:** 在Windows 10上的Internet Explorer 11中修復視頻停機。

· **19761:** 修復HLS的ABR問題。

· **19780:** 使用Mozilla Firefox v53中損壞的HLS內容修復Ad回放。

· **1987和19744:** 這些問題解決了在搜索操作之後選擇比特率時的不一致性。 現在，在搜索時的比特率選擇是當前比特率和啟動時的比特率的較低值。

· **1981:** 在搜索3-4次後，將無限時間顯示「回放卡住」和「緩衝覆蓋」。

· **1984年：** 確認符合Chrome 59 Beta驗證介質路徑(VMP)要求。 bTVSDK能夠使用Chrome 59 Beta回放Widevine DRM內容。

· **19916:** UI-Framework上的DRM回放已中斷。 現在，它調用acquireLicense，即使元資料中沒有策略。

**2.4.8版中修復的問題**

以下問題已在Browser TVSDK 2.4.8版中解決：

· **10075**:在時間線之前查找時，未在Firefox和Chrome上接收到播放完整事件，在Firefox上未收到查找事件。

· **15775**:在Windows 8.1 Internet Explorer上播放未接收的完整事件。

· **17306**:對於SSAI流，支援回放。 不支援跟蹤縫合廣告。

· **19142**:有時倒帶會導致視頻播放器永遠處於緩衝狀態。

· **19218**:UI框架中不提供廣告標籤。

· **19219**:只播放廣告不能通過UI框架運行。

· **19222**:對播放清單請求一次AES-128密鑰，然後從快取中提供後續請求。 早些時候，每段都會收到請求。

· **19597**:&quot;未捕獲的TypeError:無法讀取未定義的屬性「log」」，Chrome canary生成。

· **19605**:adRequestDomain在Flash回退模式下不可用。

· **19608**:未為HLS Live流插入VMAP廣告。 SDK現在考慮提示標籤，而不依賴於VMAP響應中的時間偏移值。

· **19637**:廣告播放在廣告結束時會導致指令碼錯誤。

· **19732**:CRS播放清單請求失敗，出現404錯誤。 現在，瀏覽器TVSDK的1401和1403請求已更新，以便處理。

· **19762**:acquireLicense在setAuthenticationToken之前調用，因為無論令牌有效性如何，都返回了有效的許可證。 現在已修復此問題，並且僅在setAuthenticationToken響應後調用acquireLicense。

**2.4.7版中修復的問題**

2.4.7版中修復了以下問題：

· **8397**:如果段不以關鍵幀開頭，則通過Adobe Medium伺服器生成的HLS Live流可能不會播放。

· **13606**:已修復Chrome瀏覽器上HLS流的多個Seek相關問題。

· **14807**:在Chrome瀏覽器上，如果在play()後立即觸發查找或暫停，則播放可能會停止，並出現錯誤DOMException:play()請求被調用中斷……（鉻問題# 593273）。

· **19085**:MediaPlayer參數（如卷、abrControlParameters和ccStyle）在重置播放器時未設定為預設值。

**2.4.6版中修復的問題**

在2.4.6版中修復了以下問題：

· **18093**:當您在Flash Player回退模式下使用Flash版本24時，將返回訂閱標籤旁邊的標籤的TimedMetadata。

**2.4.4版中修復的問題**

2.4.4版中修復了以下問題：

· **8711**:使用MSE時，預設情況下608/708字幕保持正確。

· **13934**:播放HLS Live流時，不適用廣告的ABR設定。

· **14079**:具有低DVR窗口的HLS Live流的壽命可能會失敗，因為由於網路延遲問題，回放可能會落後。 按一下即時點以繼續播放。

· **15037**:播放器UI框架附帶的示例在Windows 7的MicrosoftInternet Explorer 10上不起作用。

· **15913**:對於HLS VOD流，在Chrome上，如果清單響應未修改304，則流將不會播放。 自Chrome v55(Crim issue 633696)起，此問題就已修復。

· **16103**:在Android Chrome上，在低頻寬條件下，回放可能會因未捕獲的TypeError而停止：無法讀取未定義錯誤的屬性「programDateTime」。

· **16265**:對於HLS VOD和Live流，跨不連續點尋找是行不通的。

· **16709**:使用PDT和不連續標籤恢復HLS Live流可能會導致玩家在緩衝中卡住。

## 已知問題和限制 {#known-issues-and-limitations}

下面介紹了瀏覽器TVSDK中的限制和已知問題。

**表16:核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5在Firefox、IE、Chrome、Android Chrome中</strong></td> 
   <td><strong>HTML,iOS野生動物園</strong></td> 
   <td><strong>Chromecast（僅DASH回放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>常規播放（播放、暫停、查找）</td> 
   <td><p>·不支援HLS以外的媒體格式。</p> <p>8799:Flash回退不會處理混合內容，因此需要確保內容、廣告和其他URL不會導致混合內容（安全內容和不安全內容一起使用）。</p> <p>· 19271:在Flash回退模式下不支援通過UI框架進行多視圖回放。</p> <p>·Flash回退在Windows 7上的MicrosoftInternet Explorer 8和9上不起作用，因為SDK不支援這些版本。</p> <p>· 20262:Flash回退將自定義參數添加到目標資訊清單。 同時，在Flash和均方誤差情況下，自定義參數的優先順序順序也不同。</p> <p>· 20653：瀏覽器TVSDKFlash回退在Win10上無法使用Creators Update。</p> <p>·Flash回退與Flash Player版本23及更高版本配合使用。</p> <p>· 20087 - Chrome 59 Beta</p> <p>Flash25.0.0.171</p> <p>Beta（預設）,HLS回放在Flash回退模式下不工作。 在加那利上行得通。</p> </td> 
   <td><p>· 12563:由於MPD中不支援音頻編解碼器字串，帶音頻編解碼器的Dash Streams mp4a.40.02在Firefox上不會播放。 支援音頻編解碼器mp4a.40.2。</p> <p>15029:在UI-Framework中的multiView中切換視頻時，播放/暫停按鈕不會相應地更新。</p> <p>· 16034：在Windows 8.1 IE上，調用reset()會導致未知MIME類型錯誤。 請重新載入媒體以繼續播放。</p> <p>· 18235:DASH視頻點播流在Ads上出現了一些尋道問題。</p> <p>· 18727:MSE不支援錯誤API</p> <p>18750:在某些情況下，SDK和UI框架的狀態更改事件可能無序，在UI框架中，載入資源後添加的事件偵聽器可能缺少IDLE和Initializing StatusChange事件。</p> <p>· 18889:如果MediaPlayer處於ERROR狀態，則不返回視圖對象。</p> <p>· 19039:如果是AdobePSDK。 媒體播放器。 seekToLocal()與大於EOF的值一起使用，如果為MSE，則從頭開始回放。</p> <p>· 19049:在播放期間阻止視頻時，Chrome、IE和Firefox上未報告Flash Player錯誤狀態。</p> <p>· 17205:在播放未混音流時視頻播放停止數小時，而音頻繼續播放(Crrim issue# 664033)。</p> <p>· 12308:指定composition_time_offset的DASH流可能在Chrome瀏覽器上將timeStampOffset應用到它，導致負解碼時間，因此出現MEDIA_ERR_SRC_NOT_ SUPPORTED錯誤(Crir issue #398141)。</p> <p>· 14126:由於MSE源緩衝區中的內部間隙，Firefox（問題# 1316024）上的回放可能會停止。 嘗試查找以繼續播放。</p> <p>· 19115:MS Edge和IE 11（Win 8.1和10）未在CORS重定向時將「原點」設定為空，但因頭不為空而失敗，導致回放錯誤。</p> <p>· 19861：在已播放的媒體的源緩衝區上附加行為問題。 Chrome拒絕附加的片段，包括moov，導致後續解碼錯誤。 (鉻問題#735335)</p> <p>19921:某些HLS內容的回放停止，即使其緩衝成功(Cr問題#713540)</p> <p>· 20444：在IE和Edge上尋求緩衝範圍的結束可能會導致播放停止。</p> <p>· 20511:有時，對於有或沒有廣告的HLS流，可以觀察到查找拒絕。</p> <p>· 20743:在Windows 10 Chrome上，HLS Live流在MP4預滾回放前播放幾秒鐘。</p> <p>· 21043:由於缺少元資料，初始載入時視頻維度可能不正確。</p> <p>· 2115:如果播放清單中的視頻可以預滾動廣告，則需要Android用戶手勢來開始播放。</p> <p>· HLS Live不支援時間戳滾動更新。</p> <p>·不支援AAC-SSR音頻。</p> <p>不支援音頻編解碼器AC3和增強型AC3。</p> <p>·對於具有時間戳間斷但沒有間斷標籤的流</p> <p>·由於跳轉，播放可能出現故障和查找錯誤。</p> <p>·內容持續時間和播放持續時間可能不匹配。</p> <p>·表示形式和格式副本之間的不連續性應與其他形式相匹配，可能導致同步和停滯問題。</p> <p>·字幕和WebVTT可能不會靠近流的結尾。</p> <p>·不支援跨時間戳跳轉更改音頻編解碼器。</p> <p>·不支援廣告插入。</p> <p>·快速轉發特技模式可能導致Win 8.1 IE 11上出現回放循環(MS問題#12446268)。</p> <p>破折號：</p> <p>·對於即時流 — 支援動態類型的即時配置檔案。</p> <p>·對於VoD流 — 支援靜態類型的即時配置檔案。</p> <p>對於VoD流 — 未針對廣告工作流對按需配置檔案進行認證。</p> </td> 
   <td><p>·不支援DASH Live和DASH視頻點播流。</p> <p>·iOS全屏模式不支援PIP（畫中畫）視頻播放。</p> <p>在Safari（視頻標籤）擴展上，沒有正確內容類型標頭的較少清單無效。</p> </td> 
   <td><p>·發送程式應用中的應用程式ID必須與將接收程式的URL註冊為自定義接收程式時生成的應用程式ID相同。</p> <p>·參考播放器經DASH工作流認證。 未驗證UI框架。</p> <p>有關支援的媒體編解碼器的清單，請參閱 <a href="https://developers.google.com/cast/docs/media"><em>這裡</em></a>。</p> </td> 
  </tr> 
  <tr> 
   <td>FER視頻點播</td> 
   <td>常規播放（播放、暫停、查找）</td> 
   <td> </td> 
   <td>18098:在HLS LBA FER流中觀察到一些尋道問題。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>自適應比特率</td> 
   <td><p>· 20079:緩衝區在緩衝範圍內的尋道時重寫緩衝區。</p> <p>20080:FlashABR行為與MSE一致。</p> </td> 
   <td><p>·由於與緩衝區相關的限制，ABR流中的僅音頻回退變數被忽略。</p> <p>· 12289:ABR控制參數在HLS/DASH流未混合的情況下不適用於音頻。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>608/708字幕</td> 
   <td> </td> 
   <td><p>· 7810:在Android 4.4.4上，Chrome似乎不支援播放器使用的基本CSS字型系列，因此字型樣式更改功能無效。</p> <p>·若有608個字幕，則CC頻道不能更改。</p> <p>· 608個字幕不支援高級樣式功能。</p> <p>支援通過輔助工具標籤發出信號的嵌入字幕(608/708)。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206:播放器在顯示字幕時會忽略WebVTT檔案中的區域標籤。</p> <p>·破折號：不支援分段/分段VTT檔案。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>清單故障轉移</td> 
   <td>21056:使用Flash回退，如果主流在回放期間返回404錯誤，則Live流不會發生故障轉移。</td> 
   <td>清單故障切換僅適用於內容，而不適用於廣告。</td> 
   <td>缺少的播放清單故障轉移僅在Safari上對HTTP錯誤代碼404起作用。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>高級故障切換</td> 
   <td> </td> 
   <td><p>·段故障切換不支援跳過不可用的段並繼續回放。</p> <p>20533:播放清單中缺少的段應視為「不連續」，應從下一個可用段恢復回放。</p> <p>21267:由於故障轉移而進行的流交換可能會導致下載較舊的段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>QoS和播放器通知</td> 
   <td>21129:幀速率在Flash回退時不可用。</td> 
   <td><p>· 11170:</p> <p>Timed_Event不適用於MSE的瀏覽器TVSDK，而不適用於Flash回退的瀏覽器TVSDK。</p> <p>21129:不計算即時流的幀速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>支援Cookie標頭</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Safari不支援withCredentials標誌和cookie標頭。</p> <p>21051:要允許Safari中的Cookie，請從「首選項」&gt;「隱私」中啟用「Cookie和網站資料」設定。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>自定義標籤</td> 
   <td>14763:不支援以#開頭的自定義標籤。 現在，在Flash回退期間，將建立並報告此類標籤的TimedMetadata對象。</td> 
   <td>未驗證帶內自定義標籤的流。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>延遲綁定音頻</td> 
   <td> </td> 
   <td><p>· HLS Live LBA流不支援廣告插入。</p> <p>· 17273:HLS VOD LBA流在發生故障切換時切換到預設格式副本，無法切換回上次選擇的格式副本。</p> <p>· 20251:HLS Live LBA流可能在尋找時停滯。</p> <p>· 20497:如果HLS LBA未混合流在接近流結尾處缺少音頻或視頻幀，則播放器仍處於緩衝狀態。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302重定向</td> 
   <td> </td> 
   <td><p>15787:302</p> <p>Windows Edge和IE瀏覽器不支援重定向優化，因為這些瀏覽器不支援XMLHttpRequest對象中的responseURL屬性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17:高級回放功能**

<table> 
 <tbody> 
  <tr> 
   <td>內容類型</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>HTML5在Firefox、IE、Chrome、Android Chrome中</strong></td> 
   <td><strong>HTML,iOS野生動物園</strong></td> 
   <td><strong>Chromecast（僅DASH回放）</strong></td> 
  </tr> 
  <tr> 
   <td>視頻點播</td> 
   <td>偏移處回放</td> 
   <td><p>不支援以特定偏移值開始播放MP4內容。</p> </td> 
   <td>20492:在從偏移值恢復內容之前播放偏移前的中間卷廣告。</td> 
   <td>在iOS上不支援使用偏移功能播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>視頻點播</td> 
   <td>特技遊戲</td> 
   <td>「平滑滴播」不適用於沒有iFrame格式副本的流。</td> 
   <td><p>· Firefox和Internet Explorer不支援特技播放調整，因此這些瀏覽器不提供反向特技模式。</p> <p>·在播放內容和廣告時，不提供特技播放。</p> <p>· 10435:在DASH播放期間，Internet Explorer上的前向特技播放中視頻凍結(Win 8.1)</p> <p>間歇性。 這是因為我們使用了視頻元素playbackRate屬性，而沒有特技播放適配。</p> <p>14182:有時，在Chrome瀏覽器上倒帶期間，可能無法接收查找事件，因此特技模式將無法工作。</p> <p>· 14942:即使在非特技播放流的情況下，也可以在Chrome上為Android設定播放速率，但不會應用設定，且播放將以正常速率繼續。</p> <p>· 17308:在Trickplay模式下，Seek不工作。</p> <p>· 17309:在Chrome瀏覽器上，反向特技模式不能持續超過2秒。</p> <p>19272:在DASH流的情況下，特技播放可能無法從Windows 10邊緣瀏覽器上的緩衝恢復。</p> </td> 
   <td>不支援倒帶特技模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>ID3分析</td> 
   <td>20346:SDK還應返回ID3幀的文本編碼位元組。</td> 
   <td><p>SDK忽略音頻資料傳輸流(ADTS)中可用的ID3標籤。</p> <p>· 12378:ID3定時元資料在Flash和瀏覽器上以MSE支援在不同時間被解析，因此參考播放器時間線上的顯示行為也不同。</p> <p>· 19247:UI框架不支援ID3分析。</p> </td> 
   <td><p>· 20323:Safari未分析用於指示aac段第一個樣本時間戳的PRIV ID3標籤(Safari問題#32422733)</p> <p>· 20350:在某些設備(包括MACOS X 10.1、iPad10)上，Safari在特技模式下不提供提示更改事件，因此未接收ID3幀。 (Safari問題#32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>不連續標籤支援</td> 
   <td> </td> 
   <td><p>·包含不連續的HLS流不支援客戶端和插入。</p> <p>· HLS流中不允許跨中斷更改音頻編解碼器。</p> <p>·帶不連續標籤的HLS流不支援音頻跟蹤開關</p> </td> 
   <td>不連續序列號是合肥光源在Safari上回放時對不連續流的要求。</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表18:內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5在Firefox、IE、Chrome、Android Chrome中</strong></td> 
   <td><strong>HTML,iOS野生動物園</strong></td> 
   <td><strong>Chromecast（僅DASH回放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>AES-128加密內容不支援位元組範圍。</td> 
   <td>12324:如果未指定IV標籤，則HLS AES-128加密流無法在Safari上回放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>視頻點播</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660:HTML5播放器對過期的PlayReady加密破折號內容引發內部伺服器錯誤。</p> <p>· 16720:如果缺少句點標籤中的起始屬性，則DASH DRM加密內容將無法工作。</p> <p>· 18589:帶Xlink的受DRM保護的短划線VoD多時段流不支援回放。</p> <p>· 18653:多鍵Widevine MultiPeriod內容的回放在第一個時段停止，無法切換到下一個時段。</p> <p>· 18656:Playready MultiPeriod流，使用不同密鑰加密，無法回放。</p> <p>Playready 2.0 for Dash未獲得認證。</p> <p> </p> <p> </p> </td> 
   <td>12602:HLS Fairplay DRM元資料由Safari上的HTML5播放器重複刷新</td> 
   <td><p>可以播放通過Bento4打包的DASH Widevine DRM內容。 通過Offline Packager和Shaka打包器打包的內容不會播放。 不支援DASH PlayReady DRM。</p> </td> 
  </tr> 
 </tbody> 
</table>

**表19:核心Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5在Firefox、IE、Chrome、Android Chrome中</strong></td> 
   <td><strong>HTML,iOS野生動物園</strong></td> 
   <td><strong>Chromecast（僅DASH回放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>前/中/後</td> 
   <td> </td> 
   <td><p>·使用HLS即時內容的預卷廣告以雙播放器模式播放。</p> <p>·不支援包含HLS內容的DASH廣告和包含DASH內容的HLS廣告。</p> <p>· 19002:在具有MSE adBreak的HTML5播放器中。 insertionType不返回正確的值來描述正確的插入類型，即客戶端插入和伺服器插入。</p> <p>7794:在全屏模式下顯示預設控制欄的移動設備(iOS、Chrome 33或更低版本或本機瀏覽器的Android)上，搜索欄和快進按鈕在廣告播放時可用。</p> <p>· 11048:在媒體源擴展的情況下，從ad切換到HLS Live內容不會平滑。</p> <p>· 16083:在Android 4.4 Chrome v52上，HLS和HLS內容的廣告在停止播放後有時會導致流水線解碼錯誤。</p> <p>· 16097:未處理廣告中斷期間遇到的錯誤，可能導致主流停止播放。</p> <p>· 18095:HLS即時內容不支援MP4廣告。</p> <p>19120:在HLS廣告上使用HLS內容的多個尋道可能導致流停止回放。</p> <p>· 19131:在從預滾和分段切換到內容時，可能會出現緩衝覆蓋。</p> <p>· 20296:在HLS Live流中，在DVR窗口中重新查找，然後重新查找已解決的中間輥，可能會導致回放停滯。</p> <p>· 20298:HLS中間輥即時流在第一中間輥停止時移出DVR窗口。</p> <p>· 20317:當切換到下一個廣告或從廣告切換到內容時，HLS Live流可能會停止，以防廣告中斷包含多個廣告。</p> 
    <ul> 
     <li>未解析HLS Live流的DVR窗口中的廣告。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>廣2.0/3.0</td> 
   <td> </td> 
   <td>SDK不遵守VAST adSource的VMAP響應中的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>廣2.0/3.0</td> 
   <td> </td> 
   <td>20779:SDK不遵守VAST adSource的VMAP響應中的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014:不支援VMAP重複屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>創意重新包裝</td> 
   <td> </td> 
   <td>21464:如果創意重新包裝在廣告分段中的一個廣告失敗，則完全放棄廣告響應。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表20:高級Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5在Firefox、IE、Chrome、Android Chrome中</strong></td> 
   <td><strong>HTML,iOS野生動物園</strong></td> 
   <td><strong>Chromecast（僅DASH回放）</strong></td> 
  </tr> 
  <tr> 
   <td>視頻點播</td> 
   <td>僅廣告</td> 
   <td> </td> 
   <td>20056:播放器技術屬性不相關，因為它基於主內容，在只播放廣告的情況下該內容為空</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>自定義廣告策略</td> 
   <td> </td> 
   <td><p>· MP4廣告和MP4內容不支援廣告行為。</p> <p>· 13973:自定義廣告行為 — SKIP策略在與MSE一起使用時不會引發完整事件。</p> <p>· 14939:自定義廣告行為策略跳過和跳過廣告中斷對DASH內容無效。</p> <p>· 17131:廣告的第一幀可見，在SKIP廣告中斷策略的情況下，內容將恢復。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>伴侶廣告/橫幅廣告/可點擊廣告</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>使用引用播放器時，橫幅廣告不可見。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID廣告不支援廣告行為。</p> <p>· 15032:不支援在廣告分段中與MP4或HLS廣告結合的VPAID廣告。</p> <p>· 19001:在Android和iOS上，VPAID廣告以MP4為主內容播放時，雙音軌可聽，主內容之一，廣告之一。</p> <p>· 20762:畫中畫(PIP)不支援VPAID廣告。</p> <p>· 21172:沒有為HLS VOD內容接收帶VPAID廣告的播放完整事件。</p> <p>· 21173:沒有為HLS VOD內容和後滾VPAID廣告接收onAdBreakCompleteEvent。</p> </td> 
   <td>播放器在正常模式和全屏模式之間切換，同時在VPAID廣告和主內容之間切換。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21:整合**

| **內容類型** | **功能** | **Flash** | **HTML5在Firefox、IE、Chrome、Android Chrome中** | **HTML,iOS野生動物園** | **Chromecast（僅DASH回放）** |
|---|---|---|---|---|---|
| VOD + Live | Adobe AnalyticsVHL整合 |  | 19004:無法通過UI配置器工具進行視頻分析跟蹤。 |  |  |

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://experienceleague.adobe.com/docs/primetime.html) 的子菜單。
