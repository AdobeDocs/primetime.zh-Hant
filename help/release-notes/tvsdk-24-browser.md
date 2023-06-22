---
title: 瀏覽器TVSDK 2.4發行說明
description: 瀏覽器TVSDK 2.4發行說明說明說明瀏覽器TVSDK 2.4支援和不支援的新功能和已知問題。
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

瀏覽器TVSDK 2.4發行說明說明說明瀏覽器TVSDK 2.4支援和不支援的新功能和已知問題。

## 簡介 {#introduction}

瀏覽器TVSDK是工具組，可讓您新增進階視訊播放功能、內容保護和廣告至瀏覽器視訊播放器應用程式。

瀏覽器TVSDK 2.4提供JavaScript API以建置瀏覽器視訊應用程式，並包含下列模式的播放支援：

* 僅限HTML5
* 具有自動快閃後援的HTML5
* 一律Flash

此版本包含下列資訊：

· [瀏覽器TVSDK API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [瀏覽器TVSDK程式設計手冊](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [TVSDK for 1.4 DHLS至瀏覽器TVSDK 2.4移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [從瀏覽器TVSDK 2.4.6轉換至2.4.7版](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

·包含在組建中的參考實作。

>[!NOTE]
>
>*如需此版本安全性考量的完整清單，請參閱安全性考量。

## 新增功能與支援的功能 {#what-s-new-and-supported-features}

此版本的瀏覽器TVSDK提供可用來增強視訊應用程式的新功能。

**2.4.12更新中的新增功能（版本編號204）**

瀏覽器TVSDK 2.4.12更新（版本編號204）提供下列新增功能：

* AdobePSDK.MediaPlayer的音量API實作已變更為允許在播放停用時自動在iOS上播放。

·新的API、 `auditudeSettings.ignoreVPAIDAds`，以允許忽略從Auditude伺服器接收的VPAID廣告。 API無法用於Flash遞補。

**版本2.4.11**

下列增強功能和新增專案屬於瀏覽器TVSDK 2.4.11版：

· MSE和Flash遞補模式支援HLS即時區段容錯移轉。

·支援 `AuditudeSettings.creativeRepackagingDomain` API現在也可供MSE使用。 先前僅支援Flash遞補模式。

·此版本包含嚴重客戶問題的修正。 另請參閱 *已修正的問題* 清單。

**版本2.4.10**

下列增強功能和新增專案屬於瀏覽器TVSDK 2.4.10版：

· TVSDK提供enableLogging()來啟用或停用記錄。 請參閱 [API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)以取得使用狀況。

·使用Adobe Analytics時，TVSDK不再支援預設章節。 使用您的應用程式定義和管理章節。

·此版本包含嚴重客戶問題的修正。 請參閱*已修正的問題*a清單。

**版本2.4.9**

下列增強功能和新增專案屬於瀏覽器TVSDK 2.4.9版：

·支援HLS VOD和即時串流，其具有時間不連續性，但不具不連續性標籤。

· HLS VOD和即時資料流的Safari視訊標籤支援ID3 v2.4.0影格。

·安全廣告載入實作可確保廣告伺服器呼叫根據API設定升級為安全的HTTP。 如需詳細資訊，請參閱AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration類別。 Flash遞補模式不支援此功能。

·與VAST 3.0回應相關聯的廣告ID和擴充功能資訊，現在可由TVSDK提供給應用程式，且可用來實作廣告測量的Moat整合。 如需詳細資訊，請參閱AdobePSDK.NetworkAdInfo API 。 Flash遞補模式不支援此功能。

· AdobePSDK.ForceHttpsConfiguration類別已無法使用。 成功者為

AdobePSDK.ForceHttpsAdConfiguration類別。

·新的API AdobePSDK.optimizeFlashCalls現在可用於最佳化呼叫，以改善Flash遞補模式中的HLS播放體驗。 預設為停用。

**2.4.8更新中的新增功能（版本編號6002）**

此更新包含嚴重客戶問題的修正。 另請參閱 *已修正的問題*，以取得清單。

**版本2.4.8**

下列增強功能和新增專案屬於瀏覽器TVSDK 2.4.8版：

· SDK現在與Chrome EME相容，且從Chrome v58開始提供最佳實務變更。 如需詳細資訊，請參閱 [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI Framework現在支援在Flash、僅限廣告和目標定位資訊工作流程上使用HLS存取DRM。

· setDRMAuthenticateData API已新增至UI Framework。 若要播放受Adobe存取DRM保護的資料流，請叫用此API。 或者，也可以在播放器中指定drmAuthenticateData屬性。 另請參閱 [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)以取得詳細資訊。

**版本2.4.7**

下列是2.4.7版的新功能：

·在UI架構中新增UI設定器

您可以透過下列其中一種方式來設定播放器：

· JSON物件

·使用API

為協助產生JSON物件，瀏覽器TVSDK提供**UI配置器**工具。

在此工具中，您可以選取各種設定，按一下**測試設定**以驗證設定，然後按一下**下載設定**以下載設定。 下載檔案後，您可以將此檔案的內容當作JSON物件傳遞至ptp.videoPlayer API。

·將MediaPlayerItemConfig API新增至UI架構

您可以透過MediaPlayerItemConfig設定各種功能，包括advertisingMetadata、advertisingFactory、adSigningMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscribeTags、adTags、thumbnailScrubber、billingMetricsConfiguration。 如需詳細資訊，請參閱「 」中的AdobePSDK.MediaPlayerItemConfig檔案 [瀏覽器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

在UI Framework中，已修改透過播放器設定傳遞網路設定的方式。

**版本2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**版本2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* 在UI框架中支援DRM和Analytics工作流程

DRM設定和Analytics追蹤可透過UI Framework啟用。

* 新增 `AdobePSDK.embedSWFinFullScreenDiv` API

這個新API讓播放器應用程式能夠靈活地選取可以內嵌FlashFallback.swf檔案的div。

* 已取代 `getVersion`API來源 `AdobePSDK.MediaPlayer` 類別 `AdobePSDK.Version` 類別以取得TVSDK版本相關資訊。 如需詳細資訊，請參閱 `AdobePSDK.Version` API [此處](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**版本2.4.6**

下列是2.4.6版的新功能：

* **瀏覽器支援**

Browserify可讓您在瀏覽器中使用node.js樣式模組。 您可以定義相依性，且Browserify會將所有內容整合到一個JavaScript檔案中。

* **帳單**

在計費的協助下，瀏覽器TVSDK可以收集播放器使用量度，以便對Primetime客戶計費。

>[!NOTE]
>
>Enum PSDKErrorCode中已棄用的列舉MediaPlayer.Events和已棄用的常數已在2.4.6版中移除。如需詳細資訊，請參閱 [從瀏覽器TVSDK 2.4.5轉換至2.4.6版](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**版本2.4.5**

下列是2.4.5版的新功能：

* **完整事件重播和廣告**

   HLS完整事件重播(FER)資料流現在支援廣告解析度和廣告行為。 若要啟用此支援，請將廣告訊號模式設定為 `MANIFEST_CUES` 建立 `MediaPlayerItemConfig` 物件。

* **MediaplayerView ScalePolicy支援**

   應用程式開發人員現在可以使用MediaplayerView scalePolicy屬性，為檢視指定不同的scalePolicy。

* **變形內容支援**

   使用MSE和Flash播放時，現在支援變形內容播放。

* **選擇性套用`withCredentials`**

時間 `withCredentials` 設為true，則 `Access-Control-Allow-Origin` 標頭不可設為萬用字元。 視伺服器的回應而定，瀏覽器TVSDK會選擇性地將 `withCredentials` 屬性。 如需此支援的詳細資訊，請參閱 [瀏覽器TVSDK API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**版本2.4.4**

下列是2.4.4版的新功能：

* **Chromecast範例應用程式**

此發行版本支援傳送者與接收者應用程式，可示範使用者端廣告插入的DASH VOD資料流與DASH Widevine資料流的播放。

* **進階容錯移轉支援**

此版本包含對HLS VOD資料流的進階容錯移轉使用案例（區段和伺服器容錯移轉）的支援。

**版本2.4.3**

下列是2.4.3版的新功能：

* **虛線VOD的自訂標籤**

   內嵌自訂標籤（事件）可以訂閱並接收為TimedMetadata物件。

* **沒有擴充功能的資料流播放**

   現在支援不含擴充功能的HLS和DASH資料流。 對於資訊清單檔案，載入資源時需要指定resourceType。 對於區段和VTT檔案，系統會使用Content-Type回應標頭來決定內容型別。

**版本2.4.2**

下列是2.4.2版的新功能：

* **API同位檢查**

如需API同位檢查的完整清單，請參閱 [TVSDK for 1.4 DHLS至瀏覽器TVSDK 2.4移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Sample-AES支援**

   此版本新增對MSE和Flash遞補上的Sample-AES加密內容播放的支援。 已移除在Google Chrome上透過安全來源託管AES內容的要求。

* **支援AAC容器**

   現在支援以.aac副檔名播放檔案。 這可以是純音訊串流或替代音訊。

   >[!NOTE]
   >
   >尚不支援AC3和增強型AC3轉碼器。

* **標籤化的資料流播放**

透過內容傳遞網路(CDN)傳遞的HLS資料流有時可以使用資訊清單和區段請求上的驗證權杖進行驗證，這些權杖可以作為URL引數或Cookie標頭提供。 現在支援播放這類串流。

**版本2.4.1**

下列是2.4.1版的新功能：

* **UI框架**

此架構旨在加速JavaScript型視訊播放器應用程式的UI開發，包含的API可包含播放/暫停和音量等基本控制項，以及可輕鬆新增或移除推移列狀態和隱藏式字幕設定等元素。 您可以指定與控制項相關聯的行為、建立自訂控制項，並讓播放器UI具有外觀。 這都是透過框架進行的，不需要直接操控DOM結構。

* **即時資料流的HLS播放增強功能**

此版本支援廣告插入所導致的不連續性。 它會使用EXT-PROGRAM-DATE-TIME標籤，後面接著EXT-MEDIA-SEQUENCE標籤，以跨最適化位元速率設定檔進行同步，以便順利播放。

* **VPAID 2.0支援**

影片播放器廣告服務介面定義(VPAID) 2.0版為使用者提供豐富的媒體體驗，並可讓發佈者更妥善地鎖定廣告、追蹤廣告印象，以及從影片內容獲利。 此版本支援線性JavaScript VPAID廣告隨選影片(VOD)內容。

* **自訂HLS標籤**

媒體串流可以播放清單/資訊清單檔案中的標籤形式攜帶其他中繼資料。 瀏覽器TVSDK可讓您指定及訂閱其他標籤，並在這些標籤出現在資訊清單中時收到通知。

* **在播放器時間軸上顯示的廣告標籤**

此版本支援在播放器時間軸上為VOD和即時內容顯示廣告標籤。 您可以在參考播放器中看到此行為。

**2.4支援**

2.4版提供下列功能：

* **MP3音訊播放**

   此版本支援瀏覽器上使用Media Source Extensions (MSE)和Safari視訊標籤播放MP3音訊。

* **MP4視訊播放**

   支援下列功能：

   * 單一資料流播放
   * 具有廣告行為和追蹤的前置和後置MP4廣告
   * 具有廣告行為和追蹤的前置和後置HLS廣告
   * 具有廣告行為和追蹤的前段和後段虛線廣告

## 支援的平台 {#supported-platforms}

瀏覽器TVSDK對其需要執行的平台和軟體層級有特定需求。 支援的平台和軟體層級如下：

### 桌上型電腦設定 {#desktop-configurations}

* Microsoft Windows 7：

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* APPLE OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### 行動網站設定 {#mobile-web-configurations}

* Android 4.4

   * 原生瀏覽器
   * Chrome 33+

* Android 5.0

   * 原生瀏覽器
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* APPLE IOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast （第二代；僅適用於DASH播放）**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>技術</strong> </p> </td> 
   <td><p><strong>瀏覽器TVSDK影片標籤</strong><sup>1</sup></p> </td> 
   <td><p><strong>瀏覽器TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>預設技術</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>影片標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和虛線</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>影片標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和虛線</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和虛線</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
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
   <td><p>HLS、虛線</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## 功能矩陣 {#feature-matrix}

以下是此版本支援和不支援的功能的清單：

* *MP3音訊功能 — 核心播放*
* *MP4視訊功能 — 核心播放*
* *MP4視訊功能 — 核心Ad Insertion*

>[!NOTE]
>
>*在下方的功能矩陣表格中，「Y」表示目前版本支援該功能。*

### MP3音訊功能 {#mp-audio-features}

**表1：核心播放{#table-core-playback}**

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5： Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3 VOD | 一般播放（播放、暫停、搜尋） | 不支援 | Y | Y |

1瀏覽器TVSDK視訊標籤不支援串流和DRM。 並非所有瀏覽器的轉碼器和容器支援都相同。

2 Firefox 41版或更舊版本的預設值為Flash Player。

### MP4音訊功能 {#mp-audio-features-1}

**表2：核心播放**

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5： Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4 VOD | 一般播放（播放、暫停、搜尋） | 不支援 | Y | Y |

**表3：核心Ad Insertion**

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5： Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 前置滾動(MP4) | 不支援 | Y | Y |
| Ad Insertion | MP4 VOD | 後置滾動(MP4) | 不支援 | Y | Y |

如需HLS或DASH功能支援的詳細資訊，請參閱下文。

## HLS功能矩陣 {#hls-feature-matrix}

以下是瀏覽器TVSDK中HLS功能的功能對照表。

* *HLS核心播放*
* *HLS進階播放功能*
* *HLS內容保護功能*
* *HLS核心廣告插入功能*
* *HLS進階廣告插入功能*
* *HLS整合*

>[!NOTE]
>
>*在下方的功能矩陣表格中，「Y」表示目前版本支援該功能。*

### HLS功能 {#hls-features}

支援下列功能：

**表4： HLS核心播放**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>一般播放（播放、暫停、搜尋）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>一般播放（播放、暫停和搜尋）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>最適化位元速率</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>僅限VOD</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>資訊清單容錯移轉</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>進階容錯移轉</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>有限的QoS支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>支援Cookie標頭</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>設定緩衝區控制引數</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>設定最適化</p> <p>位元速率控制項</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>自訂標籤</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td>延遲繫結音訊</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>302重新導向</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
 </tbody> 
</table>

**表5：HLS進階播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>在位移處播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>純音訊播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>特技播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>ID3剖析</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>不連續標籤支援</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>代碼化的串流</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>帳單</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表6：HLS內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe存取</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>Fairplay</p> </td> 
  </tr> 
 </tbody> 
</table>

**表7： HLS核心廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>前置滾動(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>中間滾動(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>後置滾動(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>廣告解析度和行為</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>預設廣告原則</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>創意重新封裝（MP4到HLS）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表8：HLS進階廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>僅限廣告</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>目標定位引數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>自訂引數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>自訂廣告原則</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>延遲廣告載入</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>隨附廣告、橫幅廣告、可點按廣告</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**表9：HLS整合{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5： Safari、iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>整合</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>Adobe Analytics VHL整合</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 虛線特徵矩陣 {#dash-feature-matrix}

以下是瀏覽器TVSDK中DASH功能的功能矩陣。

· *虛線核心播放功能*

· *DASH進階播放功能*

· *DASH內容保護功能*

· *DASH Core廣告插入功能*

· *DASH進階廣告插入功能*

· *DASH整合*

>[!NOTE]
>
>在下方的功能矩陣表格中，Y表示目前版本支援該功能。

### 虛線特徵 {#dash-features}

支援下列功能：

**表10：虛線核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>一般播放（播放、暫停、搜尋）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>一般播放（播放、暫停和搜尋）</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>最適化位元速率</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>608/708字幕</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>容錯移轉</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>QoS和播放器通知</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>支援Cookie標頭</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>設定緩衝區控制引數</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>設定最適化位元速率控制項</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>自訂標籤(EventStream)</p> </td> 
   <td><p>僅限VOD （內嵌）</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>延遲的音訊</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>302重新導向</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**表11：虛線進階播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>在位移處播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>純音訊播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>特技播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>ID3剖析</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>多期間支援</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>代碼化的串流</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>帳單</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表12：DASH內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Chrome、Firefox 47和更新版本以及Chromecast上的Widevine</p> <p>· Windows 8.1和Edge上的Internet Explorer上的PlayReady</p> <p>· Windows Firefox適用的Primetime DRM （僅限影片）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13：DASH Core廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5 FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>前段廣告（MP4/虛線）</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>中間滾動（虛線）</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>後置式（MP4/虛線）</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>廣告解析度和行為</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>預設廣告原則</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>創意重新封裝（MP4至DASH）</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14：DASH進階廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>僅限廣告</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>目標定位引數</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>自訂引數</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>自訂廣告原則</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>延遲廣告載入</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>隨附廣告、橫幅廣告、可點按廣告</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
 </tbody> 
</table>

**表15：虛線整合**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容型別</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>HTML5：FF、IE、Chrome、Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>整合</p> </td> 
   <td><p>VOD +即時</p> </td> 
   <td><p>Adobe Analytics VHL整合</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## 已修正的問題 {#issues-fixed}

**2.4.12更新（版本編號204）中修正的問題**

瀏覽器TVSDK版本2.4.12更新（版本編號204）中修正下列問題：

· **21647**- TVSDK應允許在音訊靜音時在iOS裝置上自動播放視訊。

· **21465** — 播放DASH Live資料流後播放受DRM保護的DASH資料流時，收到「錯誤金鑰系統存取遭拒」。

· **21442** — 在使用使用者手勢播放前置廣告後，在iOS網頁上啟用內容自動播放。

· **21240** — 提供API以篩選從Auditude/VMAP剖析的VPAID廣告。

**2.4.11版中修正的問題**

瀏覽器TVSDK 2.4.11版已修正下列問題：

**核心播放功能：**

· **19192**： TVSDK現在會實作TextFormat：bottomInset和TextFormat：safeArea。 由於這些增強功能，如果熒幕上顯示控制列，隱藏式字幕可以重新定位。

· **21009**：如果跨不連續性搜尋，隱藏式字幕會持續保留在熒幕上，直到出現新字幕。

· **21141**：在附加區段期間，由於競爭條件，已拒絕向後搜尋。

· **21142**：當播放器處於初始化狀態時，讓可搜尋的播放範圍可供使用。 由於這些變更，現在支援在位置開始工作階段。

· **21363**：插入短劃線資料流的廣告後，608/708隱藏式字幕不同步。

**廣告插入功能：**

· **21179**：現在，透過正確設定ad.primaryAsset.adParameters屬性，可解決VOD內容的中段相關問題（長暫停、黑色影格）。

· **21257**：如果MP4不是有效的MIME型別，且已啟用創意重新封裝功能，則會選擇具有最高位元速率的MP4檔案進行轉碼。

· **21361**： TVSDK現在會從VAST回應傳遞廣告系統和創作ID作為創意封裝請求中的查詢引數，以支援其他標準化規則。

**2.4.10版中修正的問題**

瀏覽器TVSDK 2.4.10版已修正下列問題：

**核心播放功能：**

· **21060**：包含中斷的HLS資料流及ISO BMFF方塊執行到資料流結尾時，擲回無效的轉碼器錯誤。

· **21045**：播放清單中的第一個視訊播放完成後，自動播放無法在iOS上運作。

· **20975**：QoS提供者在Chrome瀏覽器上將影格速率傳回為NaN。

· **20823**：遇到沒有資料的區段時擲回不支援的轉碼器錯誤。

· **20769**：SDK現在會在搜尋時從目前的位元速率開始，而不是根據ABR原則立即切換。

· **20031**：在IE11 (Windows 8.1)上處於直向模式時，視訊畫面會變小。 內容保護功能：

· **19316**：略過解密失敗的區段（若是HLS AES-128資料流）。

**2.4.9版中修正的問題**

下列問題已在瀏覽器TVSDK版本2.4.9中修正：

**核心播放功能：**

· **13407**：如果Firefox在播放期間停止傳送「ontimeupdate」事件，DASH資料流可能會停頓。

· **16380**：在透過MSE播放具有不符開始時間的區段之混合音訊視訊內容期間，表示之間的音訊同步錯誤累積在ABR切換器上，最終導致錯誤(Chromium問題#663686)。

· **17985**：在Firefox瀏覽器上播放特定ISO-BMFF串流時，播放會卡住(Firefox問題#1342913)。 此問題自Firefox v53以來已修正。

· **19141**：未抓取（在Promise中） ReferenceError：未定義寬度。

· **18997， 19299**：區段邊界出現視訊閃爍問題。 這是因為SDK未正確計算最後一個範例的構成時間位移。

· **19780**：Firefox v53上的HLS內容和HLS廣告不會開始播放(Firefox問題#354653)。

· **20046**：程式日期時間接收為金鑰，而不是作為計時中繼資料物件時的值。

· **20047**： useDefaultResizeHandler擲回Flash遞補錯誤。

· **20179**：Flash遞補不適用於Flash Playerv25.0.0.171。

· **20293**：Firefox會停止緩衝某些HLS資料流的資料，導致停頓。

· **20626**：播放器因錯誤處理零持續時間的視訊範例，在Chrome上擲回媒體解碼錯誤。

· **20078**：瀏覽器錯誤「QuotaExceeded」導致播放停止。

· **18639**：在HLS即時資料流608 CC中，有時會顯示為拼字錯誤。

· **20028**： ClosedCaptions size引數不會變更字型大小。

· **20613**：隱藏式字幕方塊彼此重疊，使字幕難以辨認。

**核心Ad Insertion(CSAI)功能：**

· **20043**：缺少具有多個廣告和第三方重新導向的廣告曝光次數和廣告追蹤呼叫。

· **20044**：使用創意重新封裝時，必須成功重新封裝廣告插播中的所有廣告，否則會完全捨棄廣告插播。

· **20097**：如果廣告資訊清單不可用，則會跳過廣告播放並立即繼續主要內容，而不是等待20秒的逾時。

**在2.4.8版（版本編號6002）更新中修正的問題**

瀏覽器TVSDK版本2.4.8更新（版本編號6002）中修正下列問題：

· **14126：** 由於MSE來源緩衝區中的內部間隙，Firefox上的播放可能會停滯(問題#1316024)。 嘗試搜尋以繼續播放

· **19608：** 修正以接受來自Auditude VMAP回應的時間偏移值。

· **19635：** 修正Windows 10上Internet Explorer 11的視訊停頓問題。

· **19761：** 修正HLS的ABR問題。

· **19780：** 修正Mozilla Firefox v53中HLS內容損毀的廣告播放。

· **19877和19744：** 此問題修正搜尋作業後選取位元速率的不一致問題。 現在，搜尋時選擇的位元速率是目前位元速率和啟動時位元速率的較低值。

· **19881：** 執行3-4次搜尋後，播放停滯和緩衝覆蓋會無限期顯示。

· **19884：** 確認符合Chrome 59 Beta驗證媒體路徑(VMP)的要求。 bTVSDK能夠使用Chrome 59 Beta版播放Widevine DRM內容。

· **19916：** UI-Framework上的DRM播放中斷。 現在，即使中繼資料中沒有原則，它也會叫用acquireLicense。

**2.4.8版中修正的問題**

瀏覽器TVSDK 2.4.8版已修正下列問題：

· **10075**：在時間表之前搜尋時，未在Firefox和Chrome上收到播放完成事件，並且未在Firefox上收到搜尋事件。

· **15775**：在Windows 8.1 Internet Explorer上未收到播放完成事件。

· **17306**：對於SSAI串流，支援播放。 不支援追蹤拼接廣告。

· **19142**：有時倒帶會導致視訊播放器永遠保持緩衝狀態。

· **19218**：無法透過UI框架使用廣告標籤。

· **19219**：僅廣告播放無法透過UI框架運作。

· **19222**：對播放清單請求一次AES-128金鑰，然後從快取中提供後續請求。 之前會要求每個區段使用它。

· **19597**： Chrome Canary組建中出現「Uncated TypeError： Cannot read property &#39;log&#39; of undefined」。

· **19605**：在Flash遞補模式中無法使用adRequestDomain。

· **19608**：沒有為HLS即時資料流插入VMAP廣告。 SDK現在會考量提示標籤，不依賴VMAP回應中的時間位移值。

· **19637**：僅廣告播放會在廣告結尾導致指令碼錯誤。

· **19732**：CRS播放清單請求失敗，並出現404錯誤。 來自瀏覽器TVSDK的1401和1403請求現已更新以處理這些請求。

· **19762**：由於setAuthenticationToken之前曾呼叫acquireLicense，因此不論權杖是否有效，都會傳回有效的授權。 此問題現在已修正，且僅在setAuthenticationToken回應後呼叫acquireLicense。

**2.4.7版中修正的問題**

版本2.4.7已修正下列問題：

· **8397**：如果區段不是以關鍵框架開頭，則透過Adobe Medium伺服器產生的HLS即時資料流可能不會播放。

· **13606**：已修正Chrome瀏覽器上HLS資料流的多個搜尋相關問題。

· **14807**：在Chrome瀏覽器上，如果在play()之後立即觸發搜尋或暫停，播放可能會停止並出現錯誤DOMException： play()請求被呼叫中斷……(Chromium問題# 593273)。

· **19085**：重設播放器時，MediaPlayer引數（例如音量、abrControlParameters和ccStyle）未設定為預設值。

**2.4.6版中修正的問題**

版本2.4.6已修正下列問題：

· **18093**：當您在Flash遞補模式中使用Flash Player版本24時，會傳回訂閱標籤旁邊的TimedMetadata。

**2.4.4版中修正的問題**

版本2.4.4已修正下列問題：

· **8711**：使用MSE時，608/708字幕預設為靠左對齊。

· **13934**：廣告的ABR設定不適用於HLS即時資料流的播放。

· **14079**：具有低DVR視窗的HLS即時資料流的壽命可能會失敗，因為播放可能會因為網路延遲問題而延遲。 按一下即時點以繼續播放。

· **15037**：播放器UI架構隨附的範例無法在Windows 7上的Microsoft Internet Explorer 10上運作。

· **15913**：對於HLS VOD資料流，如果資訊清單回應為304且未修改，則在Chrome上不會播放資料流。 此問題自Chrome v55 (Chromium問題633696)以來已修正。

· **16103**：在Android Chrome上，在低頻寬條件下，播放可能會因未攔截的TypeError：無法讀取未定義錯誤的屬性「programDateTime」而停止。

· **16265**：針對HLS VOD和即時資料流，無法跨不連續範圍搜尋。

· **16709**：使用PDT和不連續性標籤恢復HLS即時資料流可能會導致播放器卡在緩衝中。

## 已知問題和限制 {#known-issues-and-limitations}

底下提及瀏覽器TVSDK的限制和已知問題。

**表16：核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容型別</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari、iOS、Safari中的HTML5</strong></td> 
   <td><strong>Chromecast （僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>一般播放（播放、暫停、搜尋）</td> 
   <td><p>·不支援HLS以外的媒體格式。</p> <p>8799：Flash遞補不會處理混合的內容，因此需要確保內容、廣告和其他URL不會導致混合的內容（安全和不安全內容合在一起）。</p> <p>· 19271：Flash遞補模式不支援透過UI框架的多重檢視播放。</p> <p>·Flash遞補無法在Windows 7上的Microsoft Internet Explorer 8和9上運作，因為SDK不支援這些版本。</p> <p>· 20262：Flash備援會將自訂引數新增到目標定位資訊清單。 此外，自訂引數的優先順序在Flash和MSE的情況下也不同。</p> <p>· 20653：瀏覽器TVSDKFlash遞補無法在具有建立者更新的Win10上運作。</p> <p>·Flash遞補可搭配Flash Player版本23或更新版本使用。</p> <p>· 20087 - Chrome 59 Beta版，含</p> <p>Flash25.0.0.171</p> <p>Beta （預設），HLS播放無法用於Flash遞補模式。 在Canary上運作正常。</p> </td> 
   <td><p>· 12563：使用音訊轉碼器mp4a.40.02的Dash Streams不會在Firefox上播放，因為MPD不支援的音訊轉碼器字串。 支援音訊轉碼器mp4a.40.2。</p> <p>15029：在UI-Framework的multiView中切換視訊時，播放/暫停按鈕未相應地更新。</p> <p>· 16034：在Windows 8.1 IE上，呼叫reset()會導致未知的MIME型別錯誤。 請重新載入媒體以繼續播放。</p> <p>· 18235：使用具有廣告的DASH vod串流時，發現某些搜尋問題。</p> <p>· 18727： MSE不支援錯誤API</p> <p>18750：在某些情況下，SDK和UI架構的「狀態變更」事件可能順序不對，而在UI架構中，載入資源後新增的事件「接聽程式」可能缺少「閒置」和「正在初始化StatusChange」事件。</p> <p>· 18889：如果MediaPlayer處於ERROR狀態，則不會傳回檢視物件。</p> <p>·19039：若為AdobePSDK。 MediaPlayer。 seekToLocal()與大於EOF的值搭配使用，若是MSE，則會從頭開始播放。</p> <p>· 19049：當視訊在播放期間遭到封鎖時，Chrome、IE、Firefox上未報告Flash Player的錯誤狀態。</p> <p>· 17205：當音訊繼續播放時，影片播放停止播放未設為靜音的資料流幾個小時(Chromium issue# 664033)。</p> <p>· 12308：指定composition_ time_offset的DASH資料流可能會在Chrome瀏覽器上套用timeStampOffset，導致負的解碼時間，因此會出現MEDIA_ERR_ SRC_NOT_ SUPPORTED錯誤(Chromium問題#398141)。</p> <p>· 14126：由於MSE來源緩衝區中的內部間隙，Firefox上的播放可能會停滯(問題# 1316024)。 嘗試搜尋以繼續播放。</p> <p>· 19115： MS Edge和IE 11 （Win 8.1和10）未在CORS重新導向上將Origin設定為null但會失敗，因為標題不是null會導致播放錯誤。</p> <p>· 19861：在已播放媒體的來源緩衝區上附加行為的問題。 Chrome會拒絕附加的片段（包括moov），導致後續的解碼錯誤。 (Chromium第#735335期)</p> <p>19921：某些HLS內容的播放停止，即使已成功緩衝(Chromium問題#713540)</p> <p>· 20444：在IE和Edge上搜尋至緩衝範圍的結尾可能會導致播放停止。</p> <p>·20511：有時候，對於有或沒有廣告的HLS資料流，可以觀察到搜尋拒絕。</p> <p>· 20743：在Windows 10 Chrome上，HLS Live資料流會在MP4前段播放之前播放幾秒。</p> <p>· 21043：由於缺少中繼資料，首次載入時的視訊維度可能不正確。</p> <p>·21115：如果播放清單中的影片有前段廣告，則需要使用Android使用者手勢才能開始播放。</p> <p>· HLS Live不支援時間戳記滑動。</p> <p>·不支援AAC-SSR音訊。</p> <p>不支援音訊轉碼器AC3和增強型AC3。</p> <p>·對於具有時間戳記不連續但不具有不連續標籤的資料流</p> <p>·由於跳躍，播放可能會出現問題和不正確的搜尋。</p> <p>·內容持續期間和播放持續期間可能不相符。</p> <p>·表示和轉譯之間的不連續情況應符合其他智慧，這可能會導致同步和延遲問題。</p> <p>·字幕和WebVTT可能不會出現在資料流結尾附近。</p> <p>·跨時間戳記跳躍不支援音訊轉碼器變更。</p> <p>·不支援廣告插入。</p> <p>·快速前進特技模式可能會導致Win 8.1 IE 11上的播放回圈(MS問題#12446268)。</p> <p>虛線：</p> <p>·對於即時資料流 — 支援動態型別的即時設定檔。</p> <p>·對於VoD串流 — 支援靜態型別的即時設定檔。</p> <p>對於VoD串流 — 隨選設定檔未針對廣告工作流程進行認證。</p> </td> 
   <td><p>·不支援DASH Live和DASH Video on Demand資料流。</p> <p>·全熒幕模式的iOS不支援PIP（子母畫面）視訊播放。</p> <p>在Safari （影片標籤）擴充功能上，沒有正確內容型別標題的較少資訊清單無法運作。</p> </td> 
   <td><p>·傳送者應用程式中的applicationID必須與將接收者的URL註冊為自訂接收者應用程式時產生的相同。</p> <p>·參考播放器已通過DASH工作流程認證。 UI架構未認證。</p> <p>如需支援的媒體轉碼器清單，請參閱 <a href="https://developers.google.com/cast/docs/media"><em>此處</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>一般播放（播放、暫停、搜尋）</td> 
   <td> </td> 
   <td>18098：發現HLS LBA FER串流存在某些搜尋問題。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>最適化位元速率</td> 
   <td><p>· 20079：在緩衝範圍內的搜尋時進行緩衝重新寫入。</p> <p>20080：FlashABR行為與MSE一致。</p> </td> 
   <td><p>·由於緩衝區相關限制，已忽略ABR資料流中的僅限音訊遞補變體。</p> <p>· 12289：未設為多址的HLS/短劃線串流時，ABR控制引數不適用於音訊。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>608/708字幕</td> 
   <td> </td> 
   <td><p>· 7810：在Android 4.4.4上，Chrome似乎不支援播放器使用的基本CSS字型系列，因此字型樣式變更功能無法運作。</p> <p>·有608個字幕時無法變更CC頻道。</p> <p>· 608字幕不支援進階樣式功能。</p> <p>支援透過Accessibility標籤訊號的內嵌註解(608/708)。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206：播放器在顯示註解時會忽略WebVTT檔案中的區域標籤。</p> <p>· DASH：不支援片段/分段VTT檔案。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>資訊清單容錯移轉</td> 
   <td>21056：透過Flash遞補，如果主要資料流在播放期間傳回404錯誤，則不會發生即時資料流的容錯移轉。</td> 
   <td>資訊清單容錯移轉僅適用於內容，不適用於廣告。</td> 
   <td>遺失播放清單容錯移轉僅適用於HTTP錯誤碼404的Safari。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>進階容錯移轉</td> 
   <td> </td> 
   <td><p>·區段容錯移轉不支援略過無法使用的區段並繼續播放。</p> <p>20533：播放清單中缺少的區段應視為中斷，並應從下一個可用區段繼續播放。</p> <p>21267：因容錯移轉而切換資料流可能會導致下載較舊的區段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>QoS和播放器通知</td> 
   <td>21129：在Flash遞補時無法使用影格速率。</td> 
   <td><p>• 11170:</p> <p>Timed_Event不適用於具有MSE的瀏覽器TVSDK，不同於具有Flash遞補的瀏覽器TVSDK。</p> <p>21129：不會計算即時資料流的影格速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>支援Cookie標頭</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Safari不支援withCredentials標幟和Cookie標頭。</p> <p>21051：若要在Safari中允許Cookie，請從「偏好設定&gt;隱私權」啟用「Cookie和網站資料」設定。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>自訂標籤</td> 
   <td>14763：不支援開頭為#以外的自訂標籤。 現在，系統會在Flash遞補期間，針對這類標籤建立和報告TimedMetadata物件。</td> 
   <td>未認證具有頻帶內自訂標籤的資料流。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>延遲繫結音訊</td> 
   <td> </td> 
   <td><p>· HLS Live LBA資料流不支援廣告插入。</p> <p>· 17273：在容錯移轉的情況下，HLS VOD LBA資料流會切換至預設轉譯，且無法切換回上次選取的專案。</p> <p>·20251： HLS即時LBA資料流可能在搜尋時停頓。</p> <p>· 20497：如果HLS LBA未設為多址的資料流在接近資料流結尾處遺漏音訊或視訊影格，播放器會維持緩衝狀態。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>302重新導向</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>windows Edge和IE瀏覽器不支援重新導向最佳化，因為這些瀏覽器不支援XMLHttpRequest物件中的responseURL屬性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17：進階播放功能**

<table> 
 <tbody> 
  <tr> 
   <td>內容型別</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari、iOS、Safari中的HTML5</strong></td> 
   <td><strong>Chromecast （僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>在位移處播放</td> 
   <td><p>不支援在特定位移值開始播放MP4內容。</p> </td> 
   <td>20492：在內容從位移值繼續之前，會播放位移值之前的中段廣告。</td> 
   <td>iOS不支援具有位移功能的播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>特技播放</td> 
   <td>沒有iFrame轉譯的資料流無法使用「平滑點播」。</td> 
   <td><p>· Firefox和Internet Explorer不支援Trick Play改寫功能，因此這些瀏覽器不提供反向特技模式。</p> <p>·將內容與廣告一起播放時，無法使用Trickplay。</p> <p>· 10435：在DASH播放期間，在Internet Explorer上繼續特技播放的視訊會凍結(Win 8.1)</p> <p>間歇性。 發生這種情況是因為我們使用的視訊元素playbackRate屬性沒有特技播放適配。</p> <p>14182：有時候，在Chrome瀏覽器上倒帶期間，可能不會收到搜尋事件，因此特技模式將無法運作。</p> <p>· 14942：即使是在非特技播放資料流的情況下，也可以在Android的Chrome上設定播放速率，但將不會套用設定，而且會以正常速率繼續播放。</p> <p>· 17308：搜尋在Trickplay模式下無法運作。</p> <p>· 17309：在Chrome瀏覽器上，反向特技模式不能持續超過2秒。</p> <p>19272：如果是DASH資料流，Windows 10 Edge瀏覽器上的緩衝可能無法復原特技播放。</p> </td> 
   <td>不支援倒帶特技模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>ID3剖析</td> 
   <td>20346： SDK也應傳回ID3框架的文字編碼位元組。</td> 
   <td><p>SDK會忽略音訊資料傳輸串流(ADTS)中可用的ID3標籤。</p> <p>· 12378：透過MSE支援，ID3定時中繼資料會在Flash和瀏覽器上的不同時間剖析，因此參考播放器時間軸上的顯示行為也會不同。</p> <p>· 19247： UI架構不支援ID3剖析。</p> </td> 
   <td><p>· 20323：Safari不會剖析用來訊號aac區段第一個樣本時間戳記的PRIV ID3標籤(Safari問題#32422733)</p> <p>· 20350：在某些裝置上(包括MAC OS X 10.1、iPad10)，Safari在特技模式下不會提供提示變更事件，因此不會收到ID3框架。 (Safari第#32450526期)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>不連續標籤支援</td> 
   <td> </td> 
   <td><p>·包含中斷的HLS資料流不支援使用者端廣告插入。</p> <p>· HLS資料流中的不連續狀況不允許音訊轉碼器變更。</p> <p>·具有中斷標籤的HLS資料流不支援音訊曲目切換</p> </td> 
   <td>具有不連續性的HLS資料流必須有不連續序號，才能在Safari上播放。</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表18：內容保護功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容型別</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari、iOS、Safari中的HTML5</strong></td> 
   <td><strong>Chromecast （僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>AES-128加密內容不支援位元組範圍。</td> 
   <td>12324：如果未指定IV標籤，HLS AES-128加密的資料流就無法在Safari上播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660：HTML5播放器擲回內部伺服器錯誤訊息給過期的PlayReady加密虛線內容。</p> <p>· 16720：如果缺少period標籤中的start屬性，DASH DRM加密內容將無法運作。</p> <p>· 18589：不支援使用Xlink播放DRM保護的Dash VoD多時段資料流。</p> <p>· 18653：使用多個索引鍵播放Widevine MultiPeriod內容，在第一時段停止，且無法切換到下一個時段。</p> <p>· 18656：播放就緒的MultiPeriod資料流，使用不同的金鑰加密，無法播放。</p> <p>Playready 2.0 for Dash未通過認證。</p> <p> </p> <p> </p> </td> 
   <td>12602： HLS Fairplay DRM中繼資料會由Safari上的HTML5播放器重複重新整理</td> 
   <td><p>可以播放透過Bento4封裝的DASH Widevine DRM內容。 透過Offline Packager和Shaka Packager封裝的內容不會播放。 不支援虛線PlayReady DRM。</p> </td> 
  </tr> 
 </tbody> 
</table>

**表19：核心Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容型別</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari、iOS、Safari中的HTML5</strong></td> 
   <td><strong>Chromecast （僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>前/中/後</td> 
   <td> </td> 
   <td><p>·含HLS即時內容的前置廣告會以Dual player模式播放。</p> <p>·不支援含有HLS內容的虛線廣告和含有虛線內容的HLS廣告。</p> <p>· 19002：在具有MSE adBreak的HTML5播放器中。 insertionType未傳回正確的值來描述正確的插入型別，即使用者端插入和/或伺服器插入。</p> <p>7794：在全熒幕模式下顯示預設控制列的行動裝置(iOS、具有Chrome 33或更低版本或原生瀏覽器的Android)上，可在廣告播放時使用搜尋列和快速前進按鈕。</p> <p>· 11048：如果是Media Source Extensions，從廣告切換至HLS即時內容會不流暢。</p> <p>· 16083：在Android 4.4 Chrome v52上，有時在播放延遲後，包含HLS內容的HLS廣告可能會導致管道解碼錯誤。</p> <p>· 16097：未處理廣告插播期間遇到的錯誤，可能會導致主資料流停止播放。</p> <p>· 18095： HLS即時內容不支援MP4廣告。</p> <p>19120：在具有HLS內容的HLS廣告上搜尋多個搜尋可能會導致資料流停止播放。</p> <p>·19131：從前段廣告插播切換為內容時，可能會顯示緩衝覆蓋。</p> <p>· 20296：若是HLS即時資料流，在DVR視窗中搜尋後接著搜尋已解析的中間捲動可能會導致播放停滯。</p> <p>· 20298：具有中間捲動的HLS即時資料流會在第一個中間捲動廣告移出DVR視窗時停頓。</p> <p>· 20317：如果廣告插播包含多個廣告，則在切換到下一個廣告或從廣告切換到內容時，HLS即時資料流可能會停滯。</p> 
    <ul> 
     <li>HLS即時資料流的DVR視窗中的廣告未解析。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK不會執行VAST adSource的VMAP回應中的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779： SDK不會接受VAST adSource的VMAP回應中的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014：不支援VMAP重複屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>創意重新封裝</td> 
   <td> </td> 
   <td>21464：如果廣告插播中的某個廣告的創意重新封裝失敗，則會完全捨棄廣告回應。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表20：進階Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容型別</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>Safari、iOS、Safari中的HTML5</strong></td> 
   <td><strong>Chromecast （僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>僅限廣告</td> 
   <td> </td> 
   <td>20056：播放器技術屬性不相關，因為其基礎是主要內容，但在僅限廣告播放的情況下為空白</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD +即時</td> 
   <td>自訂廣告原則</td> 
   <td> </td> 
   <td><p>· MP4廣告和MP4內容不支援廣告行為。</p> <p>· 13973：自訂廣告行為 — SKIP原則在與MSE搭配使用時不會擲回完成事件。</p> <p>· 14939：自訂廣告行為原則略過和略過廣告插播不適用於DASH內容。</p> <p>· 17131：廣告的第一個影格可見，然後如果SKIP廣告插播原則，則內容會繼續。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>隨附廣告/橫幅廣告/可點按廣告</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>使用參考播放器時看不到橫幅廣告。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID廣告不支援廣告行為。</p> <p>· 15032：不支援在廣告插播中搭配VPAID廣告與MP4或HLS廣告使用。</p> <p>· 19001：在Android和iOS上，當VPAID廣告以MP4播放為主要內容時，可聽到雙音軌、主要內容之一和廣告之一。</p> <p>· 20762：子母畫面(PIP)不支援VPAID廣告。</p> <p>· 21172：未收到包含VPAID廣告的HLS VOD內容的播放完成事件。</p> <p>· 21173：未收到HLS VOD內容和後置滾動VPAID廣告的onAdBreakCompleteEvent。</p> </td> 
   <td>播放器會在正常模式和全熒幕模式之間切換，同時在VPAID廣告和主要內容之間切換。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21：整合**

| **內容型別** | **功能** | **Flash** | **Firefox、IE、Chrome、Android Chrome中的HTML5** | **Safari、iOS、Safari中的HTML5** | **Chromecast （僅限DASH播放）** |
|---|---|---|---|---|---|
| VOD +即時 | Adobe Analytics VHL整合 |  | 19004：無法透過UI設定工具使用Video Analytics追蹤。 |  |  |

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://experienceleague.adobe.com/docs/primetime.html) 頁面。
