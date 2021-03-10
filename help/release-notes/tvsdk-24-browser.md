---
title: 瀏覽器TVSDK 2.4發行說明
description: 瀏覽器TVSDK 2.4發行說明說明瀏覽器TVSDK 2.4中的新功能、支援和不支援的功能及已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---


# 瀏覽器TVSDK 2.4發行說明{#browser-tvsdk-release-notes}

瀏覽器TVSDK 2.4發行說明說明瀏覽器TVSDK 2.4中的新功能、支援和不支援的功能及已知問題。

## 簡介{#introduction}

瀏覽器TVSDK是一套工具套件，可讓您在瀏覽器型視訊播放器應用程式中新增進階視訊播放功能、內容保護和廣告。

瀏覽器TVSDK 2.4提供JavaScript API來建立以瀏覽器為基礎的視訊應用程式，並包含下列模式的播放支援：

* 僅限HTML5
* HTML5含自動flash備援
* Flash永遠

此發行包含下列資訊：

· [瀏覽器TVSDK API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

· [瀏覽器TVSDK程式設計手冊](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf)。

· [1.4 DHLS的TVSDK到瀏覽器TVSDK 2.4移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

·從瀏覽器TVSDK 2.4.6轉換為2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html)版本的[。

·參考實作，包含在組建中。

>[!NOTE]
>
>*如需此版本的安全性考量事項完整清單，請參閱安全性考量事項。

## 新增功能和支援的功能{#what-s-new-and-supported-features}

本版瀏覽器TVSDK提供新功能，讓您用來增強視訊應用程式。

**2.4.12更新的新功能(Build 204)**

以下新增功能是瀏覽器TVSDK 2.4.12更新(Build 204)的一部分：

* AdobePSDK.MediaPlayer的大量API實作已變更，允許在靜音播放時在iOS上自動播放。

·新增`auditudeSettings.ignoreVPAIDAds`新API，允許忽略從Auditude伺服器收到的VPAID廣告。 API不適用於Flash備援。

**2.4.11版**

以下增強功能和新增功能是瀏覽器TVSDK 2.4.11版本的一部分：

·支援MSE和Flash備援模式的HLS Live段故障切換。

·`AuditudeSettings.creativeRepackagingDomain` API現在也支援MSE。 以前只支援Flash備援模式。

·本版本包含重要客戶問題的修正。 請參閱&#x200B;*問題已修正*&#x200B;清單。

**2.4.10版**

以下增強功能和新增功能是瀏覽器TVSDK 2.4.10版本的一部分：

· TVSDK提供enableLogging()以啟用或停用記錄。 有關用法，請參閱[API文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

·使用Adobe Analytics時，TVSDK不再支援「預設章節」。 使用您的應用程式定義和管理章節。

·本版本包含重要客戶問題的修正。 請參閱*問題已修正*清單。

**2.4.9版**

以下增強功能和新增功能是瀏覽器TVSDK 2.4.9版的一部份：

·支援具有時間不連續但沒有不連續標籤的HLS VOD和即時流。

· HLS VOD和即時串流的Safari視訊標籤支援ID3 v2.4.0影格。

·安全廣告載入實作可確保廣告伺服器呼叫已升級至根據API設定的安全HTTP。 如需詳細資訊，請參閱AdobePSDK.AdvertisingMetadata和AdobePSDK.ForceHttpsAdConfiguration類別。 Flash備援模式不支援此功能。

·與VAST 3.0回應相關的廣告ID資訊和延伸功能資訊現已由TVSDK提供給應用程式，可用於實作廣告測量的Moat整合。 如需詳細資訊，請參閱AdobePSDK.NetworkAdInfo API。 Flash備援模式不支援此功能。

· AdobePSDK.ForceHttpsConfiguration類別已不再提供。 成功者

AdobePSDK.ForceHttpsAdConfiguration類別。

·現在有新的API AdobePSDK.optimizeFlashCalls，可最佳化呼叫，以改善Flash備援模式中的HLS播放體驗。 預設會停用此功能。

**2.4.8更新的新功能(Build 6002)**

此更新包含重要客戶問題的修正。 請參閱&#x200B;*修正問題*&#x200B;以取得清單。

**2.4.8版**

以下增強功能和新增功能是瀏覽器TVSDK 2.4.8版的一部份：

· SDK現在符合Chrome EME規範，而且從Chrome v58開始提供的最佳實務變更。 如需詳細資訊，請參閱[https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· UI Framework現在支援HLS Access DRM的Flash、僅限廣告和定位資訊工作流程。

· setDRMAuthenticateData API已新增至UI架構。 若要播放使用Adobe存取DRM保護的串流，請叫用此API。 或者，也可以在播放器中指定drmAuthenticateData屬性。 如需詳細資訊，請參閱[AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)。

**2.4.7版**

以下是2.4.7版中的新功能：

·在UI架構中新增UI設定器

您可透過下列其中一種方式來設定播放器：

·使用JSON物件

·使用API

為協助產生JSON物件，瀏覽器TVSDK提供**UI設定器**工具。

在此工具中，您可以選取各種設定，按一下「**測試設定**」以驗證設定，然後按一下「**下載設定**」以下載設定。 下載檔案後，您可將此檔案的內容傳遞為JSON物件，並傳送至ptp.videoPlayer API。

·將MediaPlayerItemConfig API新增至UI架構

各種功能，包括advertisingMetadata、advertisingFactory、adSigningMode、networkConfiguration、customRangeMetadata、useHardwareDecoder、subscriber、adTags、thumbnailScrubber、billingMetricsConfig，皆可透過MediaPlayerItemConfig進行設定。 如需詳細資訊，請參閱[瀏覽器TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)中的AdobePSDK.MediaPlayerItemConfig檔案。

在UI架構中，已修改透過播放器組態傳遞網路組態的方式。

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

* 在UI架構中支援DRM和Analytics工作流程

DRM設定和Analytics追蹤可透過UI Framework啟用。

* 新增`AdobePSDK.embedSWFinFullScreenDiv` API

此新API可讓播放器應用程式靈活選擇div，以內嵌FlashFallback.swf檔案。

* 已將`AdobePSDK.MediaPlayer`類別的`getVersion`API取代為`AdobePSDK.Version`類別，以取得TVSDK版本相關資訊。 如需詳細資訊，請參閱`AdobePSDK.Version` API [這裡](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html)。

**2.4.6版**

以下是2.4.6版中的新功能：

* **瀏覽器化支援**

Browserify允許您在瀏覽器中使用node.js樣式模組。 您可以定義相依性，並且「瀏覽」將所有項目整合為一個JavaScript檔案。

* **帳單**

借助帳單，瀏覽器TVSDK可收集播放器使用量度，以向Primetime客戶收費。

>[!NOTE]
>
>Enum PSDKErrorCode中已過時的enum MediaPlayer.Events和已過時的常數已在2.4.6版中移除。如需詳細資訊，請參閱[從瀏覽器TVSDK 2.4.5轉換至2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html)版。

**2.4.5版**

以下是2.4.5版中的新功能：

* **完整活動重播和廣告**

   HLS Full Event Replay(FER)串流現在支援廣告解析度和廣告行為。 要啟用此支援，請在建立`MediaPlayerItemConfig`對象時將廣告信令模式設定為`MANIFEST_CUES`。

* **MediaplayerView ScalePolicy支援**

   應用程式開發人員現在可以使用MediaplayerView scalePolicy屬性，為檢視指定不同的scalePolicy。

* **變形內容支援**

   現在使用MSE和Flash播放時支援變形內容播放。

* **選擇性應用`withCredentials`**

當`withCredentials`設為true時，`Access-Control-Allow-Origin`標題無法設為萬用字元。 根據伺服器的回應，瀏覽器TVSDK會選擇性地設定`withCredentials`屬性。 如需此支援的詳細資訊，請參閱[瀏覽器TVSDK API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)。

**2.4.4版**

2.4.4版中有下列新功能：

* **Chromecast範例應用程式**

此版本支援傳送者和接收者應用程式，可示範播放DASH VOD串流和DASH Widevine串流並插入用戶端廣告。

* **進階容錯功能支援**

此版本包含對HLS VOD串流的進階容錯使用案例（區段和伺服器容錯）的支援。

**2.4.3版**

下列功能是2.4.3版中的新功能：

* **DASH VOD的自訂標籤**

   內嵌自訂標籤（事件）可以訂閱並接收為TimedMetadata物件。

* **播放沒有擴充功能的串流**

   現在支援不含擴充功能的HLS和DASH串流。 對於manifest檔案，在載入資源時需要指定resourceType。 對於區段和VTT檔案，「內容類型」回應標題會用來判斷內容類型。

**2.4.2版**

下列功能是2.4.2版中的新功能：

* **API奇偶校驗**

如需API奇偶校驗的完整清單，請參閱[TVSDK for 1.4 DHLS至瀏覽器TVSDK 2.4移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html)。

* **Sample-AES支援**

   此版本新增了對MSE和Flash備援的Sample-AES加密內容播放的支援。 已移除在Google Chrome上透過安全來源主控AES內容的要求。

* **支援AAC容器**

   現在支援播放副檔名為。aac的檔案。 這可以是僅限音訊的串流或替代音訊。

   >[!NOTE]
   >
   >AC3和增強的AC3轉碼器尚未受支援。

* **Token化串流播放**

透過內容傳送網路(CDN)傳送的HLS串流，有時可在資訊清單和區段要求上使用驗證Token進行驗證，而這些Token可以作為URL參數或Cookie標題提供。 現在支援這些串流的播放。

**2.4.1版**

下列功能是2.4.1版中的新功能：

* **UI架構**

此架構旨在加速JavaScript視訊播放應用程式的UI開發，其中包含API，可包含播放／暫停和音量等基本控制項，並可輕鬆新增或移除元素，例如拖曳列狀態和隱藏字幕設定。 您可以指定與控制項相關的行為、建立自訂控制項，以及設定播放器UI的外觀。 這一切都通過框架實現，而不需要直接操縱DOM結構。

* **即時串流的HLS播放增強功能**

此版本支援廣告插入造成的中斷。 它使用EXT-PROGRAM-DATE-TIME標籤，後面接著EXT-MEDIA-SEQUENCE標籤，以同步化各種可調式位元速率描述檔，以便順暢播放。

* **VPAID 2.0支援**

視訊播放器廣告服務介面定義(VPAID)2.0版為使用者提供豐富型媒體體驗，並可讓出版業者更好地鎖定廣告、追蹤廣告曝光，並從視訊內容獲利。 此版本支援視訊隨選(VOD)內容的線性JavaScript VPAID廣告。

* **自訂HLS標籤**

媒體串流可攜帶播放清單／資訊清單檔案中標籤形式的其他中繼資料。 瀏覽器TVSDK可讓您指定並訂閱其他標籤，當這些標籤出現在資訊清單中時，就會收到通知。

* **播放器時間軸上顯示的廣告標籤**

此版本支援在播放器時間軸上顯示VOD和即時內容的廣告標籤。 您可以在參考播放器中看到此行為。

**支援2.4版**

2.4版提供下列功能：

* **MP3音訊播放**

   此版本支援使用Media Source Extensions(MSE)和Safari視訊標籤在瀏覽器上播放MP3音訊。

* **MP4視訊播放**

   支援下列功能：

   * 單一串流播放
   * 包含廣告行為和追蹤的前段和後段MP4廣告
   * 具有廣告行為和追蹤的前滾和後滾HLS廣告
   * 具有廣告行為和追蹤的前段和後段虛線廣告

## 支援的平台{#supported-platforms}

瀏覽器TVSDK對其需要執行的平台和軟體層級有特定要求。 支援下列平台和軟體層級：

### 案頭配置{#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### 行動Web組態{#mobile-web-configurations}

* Android 4.4

   * 原生瀏覽器
   * Chrome 33+

* Android 5.0

   * 原生瀏覽器
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast(第二代；僅限DASH播放)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>技術</strong> </p> </td> 
   <td><p><strong>瀏覽器TVSDK視訊標</strong><sup>記1</sup></p> </td> 
   <td><p><strong>瀏覽器TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>預設技術</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>視訊標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>視訊標籤</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS和DASH</p> </td> 
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
   <td><p>HLS, DASH</p> </td> 
   <td><p>MP4和HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## 功能矩陣{#feature-matrix}

以下是此版本支援和不支援的功能清單：

* *MP3音訊功能— 核心播放*
* *MP4視訊功能— 核心播放*
* *MP4視訊功能— 核心Ad Insertion*

>[!NOTE]
>
>*在下方的功能矩陣表格中，「Y」表示目前版本支援此功能。*

### MP3音頻功能{#mp-audio-features}

**表1:核心播放{#table-core-playback}**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP3 VOD | 一般播放（播放、暫停、搜尋） | 不支援 | Y | Y |

1瀏覽器TVSDK視訊標籤不支援串流和DRM。 轉碼器和容器支援在所有瀏覽器上都不同。

2 Firefox預設為41版或更舊版本的Flash Player。

### MP4音頻功能{#mp-audio-features-1}

**表2:核心播放**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | MP4 VOD | 一般播放（播放、暫停、搜尋） | 不支援 | Y | Y |

**表3:核心Ad Insertion**

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | 預卷(MP4) | 不支援 | Y | Y |
| Ad Insertion | MP4 VOD | 後置(MP4) | 不支援 | Y | Y |

有關HLS或DASH功能支援的詳細資訊，請參閱下文。

## HLS功能矩陣{#hls-feature-matrix}

以下是瀏覽器TVSDK中HLS功能的功能表。

* *HLS Core播放*
* *HLS Advanced Playback功能*
* *HLS內容保護功能*
* *HLS核心廣告插入功能*
* *HLS進階廣告插入功能*
* *HLS整合*

>[!NOTE]
>
>*在下方的功能矩陣表格中，「Y」表示目前版本支援此功能。*

### HLS功能{#hls-features}

支援下列功能：

**表4:HLS Core播放**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
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
   <td><p>VOD + Live</p> </td> 
   <td><p>自適應位元速率</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708標題</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>僅限VOD</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>資訊清單容錯移轉</p> </td> 
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
   <td><p>支援Cookie標題</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定緩衝器控制參數</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定最適化</p> <p>位速率控制</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自訂標籤</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>延遲裝訂音訊</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302重新導向</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
 </tbody> 
</table>

**表5:HLS進階播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>在偏移處播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>純音效播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流暢的特技播放</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3剖析</p> </td> 
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
   <td><p>Token化串流</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>帳單</p> </td> 
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
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
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
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**表7:HLS核心廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>前輥(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>中輥(HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>輥後(MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>廣告解析度與行為</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預設廣告原則</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
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
   <td><p>Creative Repackaging（MP4到HLS）</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**表8:HLS進階廣告插入功能**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
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
   <td><p>VOD + Live</p> </td> 
   <td><p>定位參數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自訂參數</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自訂廣告原則</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>延遲廣告載入</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>不支援</p> </td> 
   <td><p>平台限制</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>配套廣告、橫幅廣告、可點選廣告</p> </td> 
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

**表9:HLS整合{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>類別</strong></p> </td> 
   <td><p><strong>內容類型</strong></p> </td> 
   <td><p><strong>功能</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5:FF、IE、Chrome、Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5:Safari, iOS Safari</strong></p> </td> 
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

## DASH功能矩陣{#dash-feature-matrix}

以下是瀏覽器TVSDK中DASH功能的功能表。

· *DASH核心播放功能*

· *DASH Advanced playback features*

· *DASH內容保護功能*

· *虛線核心廣告插入功能*

· *DASH進階廣告插入功能*

· *DASH整合*

>[!NOTE]
>
>在下方的功能矩陣表格中，Y表示目前版本支援此功能。

### 虛線功能{#dash-features}

支援下列功能：

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
   <td><p>VOD + Live</p> </td> 
   <td><p>自適應位元速率</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708標題</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>故障切換</p> </td> 
   <td><p>僅限VOD</p> </td> 
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
   <td><p>支援Cookie標題</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定緩衝器控制參數</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>設定自適應位元速率控制</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自訂標籤(EventStream)</p> </td> 
   <td><p>僅限VOD（內嵌）</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>後期音訊</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302重新導向</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**表11:DASH進階播放功能**

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
   <td><p>VOD</p> </td> 
   <td><p>在偏移處播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>純音效播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>特技遊戲</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>流暢的特技播放</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3剖析</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>多期支援</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Token化串流</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>播放</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>帳單</p> </td> 
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
   <td><p>Sample-AES</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>內容保護</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>· Chrome、Firefox 47和更新版本以及Chromecast上的Widevine</p> <p>·在Windows 8.1和Edge的Internet Explorer上播放就緒</p> <p>· Primetime DRM for Windows Firefox（僅限視訊）</p> </td> 
  </tr> 
 </tbody> 
</table>

**表13:DASH核心廣告插入功能**

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
   <td><p>前滾(MP4/DASH)</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>中橫(DASH)</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>後置(MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>廣告解析度與行為</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>預設廣告原則</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Creative Repackaging（MP4到DASH）</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
 </tbody> 
</table>

**表14:DASH進階廣告插入功能**

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
   <td><p>VOD</p> </td> 
   <td><p>僅限廣告</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>定位參數</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>自訂參數</p> </td> 
   <td><p>僅限VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>自訂廣告原則</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>延遲廣告載入</p> </td> 
   <td><p>不支援</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>配套廣告、橫幅廣告、可點選廣告</p> </td> 
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

## 修正的問題{#issues-fixed}

**2.4.12更新(Build 204)中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.12版更新(Build 204)中修正：

· **21647**-當音訊靜音時，TVSDK應允許在iOS裝置上自動播放視訊。

·在播放DASH Live串流後播放受DRM保護的DASH串流時，收到&#x200B;**21465**-錯誤鍵系統存取拒絕。

· **21442**-使用使用者手勢播放前置廣告後，在iOS網路上啟用內容自動播放。

· **21240**-提供的API，可篩選從Auditude/VMAP剖析的VPAID廣告。

**2.4.11版中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.11版中修正：

**核心播放功能：**

· **19192**:TVSDK現在實作TextFormat:bottomInset和TextFormat:safeArea。 由於這些增強功能，如果控制列顯示在螢幕上，隱藏字幕可重新定位。

· **21009**:隱藏字幕會持續存在於螢幕上，以避免在出現新字幕前尋找不連續字幕。

· **21141**:由於區段附加期間有競爭條件，因此反向尋道會遭拒。

· **21142**:使可查看的播放範圍在播放器處於「已初始化」狀態時可用。 由於這些變更，現在支援在位置開始作業。

· **21363**:在DASH串流的廣告插入後，608/708隱藏字幕會失去同步。

**廣告插入功能：**

· **21179**:現在可以正確設定ad.primaryAsset.adParameters屬性，解決VOD內容的中間卷相關問題（長暫停、黑色影格）。

· **21257**:如果MP4不是有效的MIME類型，並啟用創意重新封裝功能，則會選擇位元速率最高的MP4檔案進行轉碼。

· **21361**:TVSDK現在會從VAST回應傳遞廣告系統和創意ID作為創意封裝請求中的查詢參數，以支援其他標準化規則。

**2.4.10版中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.10版中修正：

**核心播放功能：**

· **21060**:HLS串流包含不連續性，而ISO BMFF包裝盒會執行至串流結尾，所引發的編碼解碼器錯誤無效。

· **21045**:在播放清單中的第一個視訊播放完成後，自動播放在iOS上無法運作。

· **20975**:Chrome瀏覽器上的QoS提供者會傳回影格速率為NaN。

· **20823**:遇到沒有資料的區段時，發生不支援的轉碼器錯誤。

· **20769**:SDK現在以目前的位元速率開始搜尋，而非根據ABR原則立即切換。

· **20031**:在IE11(Windows 8.1)上以縱向模式時，視訊畫面變小。 內容保護功能：

· **19316**:略過在HLS AES-128串流中解密失敗的段。

**2.4.9版中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.9版中修正：

**核心播放功能：**

· **13407**:如果Firefox在播放期間停止傳送「ontimeupdate」事件，DASH串流可能會停止。

· **16380**:在經由MSE播放具有不匹配開始時間的段的混音音頻視頻內容期間，ABR交換機上會累積表示之間的音頻同步錯誤，最終導致錯誤（Chromium問題#663686）。

· **17985**:在Firefox瀏覽器上播放特定ISO-BMFF串流時，播放會卡住（Firefox問題#1342913）。 自Firefox v53起，這個問題已修正。

· **19141**:未捕獲（在承諾中）ReferenceError:width is not define.

· **18997、19299**:區段邊界的視訊閃爍問題。 這是因為SDK無法正確計算上一個範例的「合成」時間偏移。

· **19780**:在Firefox v53上，HLS內容和HLS Ad無法開始播放（Firefox問題#354653）。

· **20046**:節目日期時間在作為計時元資料對象接收時，作為密鑰而不是值接收。

· **20047**:useDefaultResizeHandler會擲回錯誤，顯示Flash備援。

· **20179**:Flash備援無法與v25.0.0.171Flash Player一起使用。

· **20293**:Firefox會停止某些HLS串流的緩衝資料，導致其停止。

· **20626**:Player會在Chrome上擲出媒體解碼錯誤，因為無持續時間的視訊範例處理不正確。

· **20078**:瀏覽器錯誤「QuotaExceeded」上的播放停止。

· **18639**:在HLS Live stream 608 CC文字中，有時會顯示拼寫錯誤。

· **20028**:ClosedCaptions size參數不會變更字型大小。

· **20613**:隱藏式字幕方塊彼此重疊，使其不易辨識。

**核心Ad Insertion(CSAI)功能：**

· **20043**:遺失包含多個廣告和第三方重新導向的廣告印象和廣告追蹤呼叫。

· **20044**:使用創意重新封裝時，廣告插播中的所有廣告都必須成功重新封裝，否則廣告插播會被完全捨棄。

· **20097**:會略過廣告播放，而主要內容會立即繼續，而不是等到逾時20秒（如果廣告資訊清單不可用）。

**2.4.8版更新(Build 6002)中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.8版更新(Build 6002)中修正：

· **14126:**&#x200B;由於MSE來源緩衝區的內部間隙，Firefox上的播放可能會停止（問題#1316024）。 嘗試搜尋以繼續播放

· **19608:**&#x200B;修正以符合來自Auditude VMAP回應的時間偏移值。

· **19635:**&#x200B;修正Windows 10上Internet Explorer 11的視訊停止問題。

· **19761:** HLS的ABR問題修正。

· **19780:**&#x200B;修正在Mozilla Firefox v53中中斷的HLS內容廣告播放。

· **19877和19744:**&#x200B;這些問題修正了在搜尋操作後選擇位元速率時的不一致性。 現在，搜尋時的位元速率選擇是目前位元速率和位元速率在啟動時的較低值。

· **19881:**&#x200B;執行搜尋3-4次後，播放卡住和緩衝覆蓋會無限時間顯示。

· **1984:**&#x200B;確認符合Chrome 59測試版驗證媒體路徑(VMP)要求。 bTVSDK可以使用Chrome 59 Beta播放Widevine DRM內容。

· **19916:**&#x200B;在UI-Framework上的DRM播放中斷。 現在，它會叫用acquireLicense，即使中繼資料中沒有原則。

**2.4.8版中修正的問題**

下列問題已在瀏覽器TVSDK 2.4.8版中修正：

· **10075**:在時間軸之前搜尋時，未在Firefox和Chrome上收到播放完整事件，且在Firefox上未收到搜尋事件。

· **15775**:在Windows 8.1 Internet Explorer上播放未收到的完整事件。

· **17306**:對於SSAI串流，支援播放。 不支援縫合廣告的追蹤。

· **19142**:有時倒轉會使視訊播放器永遠處於緩衝狀態。

· **19218**:廣告標籤無法透過UI架構使用。

· **19219**:廣告播放無法透過UI架構運作。

· **19222**:AES-128密鑰被請求一次以用於播放清單，且後續請求從快取中提供。 之前會針對每個區段提出要求。

· **19597**:&quot;未捕獲的TypeError:無法讀取未定義的屬性&#39;log&#39;」。

· **19605**:adRequestDomain在「Flash備援」模式中無法使用。

· **19608**:HLS Live串流未插入VMAP廣告。 SDK現在會考慮提示標籤，而不依賴VMAP回應中的時間偏移值。

· **19637**:廣告播放只會導致廣告結尾的指令碼錯誤。

· **19732**:CRS播放清單請求失敗，出現404錯誤。 瀏覽器TVSDK的1401和1403要求現在已更新，以處理這個問題。

· **19762**:acquireLicense在setAuthenticationToken之前曾呼叫，因為傳回的有效授權與Token有效性無關。 現在已修正此問題，而acquireLicense僅在setAuthenticationToken回應後才呼叫。

**2.4.7版中修正的問題**

2.4.7版中已修正下列問題：

· **8397**:如果區段未以關鍵影格開頭，則透過Adobe Medium伺服器產生的HLS即時串流可能無法播放。

· **13606**:修正Chrome瀏覽器上HLS串流的多項搜尋相關問題。

· **14807**:在Chrome瀏覽器上，如果在play()後立即觸發搜尋或暫停，則播放可能會因錯誤DOMException而停止：play()要求已被呼叫中斷……（Chromium問題# 593273）。

· **19085**:MediaPlayer參數（例如volume、abrControlParameters和ccStyle）未設為「重設播放器時的預設值」。

**2.4.6版中修正的問題**

2.4.6版中已修正下列問題：

· **18093**:當您在「Flash Player備援」模式中使用Flash版本24時，會傳回訂閱標籤旁之標籤的TimedMetadata。

**2.4.4版中修正的問題**

2.4.4版中已修正下列問題：

· **8711**:使用MSE時，608/708字幕會依預設保持對齊。

· **13934**:播放HLS Live串流時，廣告的ABR設定不適用。

· **14079**:具有低DVR窗口的HLS Live流的使用壽命可能會失敗，因為網路延遲問題可能導致回放時間延遲。 按一下即時點以繼續播放。

· **15037**:播放器UI架構隨附的範例無法在Windows 7的Microsoft Internet Explorer 10上運作。

· **15913**:對於HLS VOD串流，在Chrome上，如果資訊清單回應未修改304，則串流將不會播放。 自Chrome v55（Chromium問題633696）起，這個問題就已修正。

· **16103**:在Android Chrome上，在低頻寬條件下，播放可能會因未擷取的TypeError而停止：無法讀取未定義錯誤的屬性&#39;programDateTime&#39;。

· **16265**:對於HLS VOD和即時串流，跨不連續點尋找無效。

· **16709**:使用PDT和不連續標籤恢復HLS Live串流可能會導致玩家在緩衝中卡住。

## 已知問題和限制{#known-issues-and-limitations}

以下提及瀏覽器TVSDK的限制和已知問題。

**表16:核心播放功能**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>iOS Safari中的HTML5</strong></td> 
   <td><strong>Chromecast（僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>一般播放（播放、暫停、搜尋）</td> 
   <td><p>·不支援HLS以外的媒體格式。</p> <p>8799:Flash後援不會處理混合內容，因此必須確保內容、廣告和其他URL不會導致混合內容（將安全與不安全的內容一起使用）。</p> <p>· 19271年：Flash備援模式不支援透過UI架構的多檢視播放。</p> <p>·Flash備援在Windows 7的Microsoft Internet Explorer 8和9上無法運作，因為SDK不支援這些版本。</p> <p>· 20262:Flash備援會新增自訂參數至定位資訊清單。 同時，在Flash和均方誤差情況下，自定義參數的優先順序順序也不同。</p> <p>· 20653：瀏覽器TVSDKFlash備援在Win10中無法使用Creators更新。</p> <p>·Flash備援可與Flash Player第23版及更新版本搭配使用。</p> <p>· 20087 - Chrome 59 Beta版，含</p> <p>Flash25.0.0.171</p> <p>Beta（預設）,HLS回放在Flash備援模式下不工作。 在加那利也沒問題。</p> </td> 
   <td><p>· 12563:具有音訊codec mp4a.40.02的虛線串流無法在Firefox上播放，因為MPD中不支援音訊codec字串。 支援音訊轉碼器mp4a.40.2。</p> <p>一五〇二九年：在UI-Framework中在multiView中切換視訊時，播放／暫停按鈕不會相應更新。</p> <p>· 16034：在Windows 8.1 IE中，呼叫reset()會導致未知的MIME類型錯誤。 請重新載入媒體以繼續播放。</p> <p>· 18235:有廣告的DASH vod串流會出現某些搜尋問題。</p> <p>· 18727:MSE不支援錯誤API</p> <p>一八七五零年：在某些情況下，SDK和UI架構的狀態變更事件可能會失序，而在UI架構中，資源載入後新增的事件監聽程式可能會遺失IDLE和初始化狀態變更事件。</p> <p>· 18889:如果MediaPlayer處於ERROR狀態，則不會傳回檢視物件。</p> <p>· 19039年：如果是AdobePSDK。 MediaPlayer。 seekToLocal()的值大於EOF，在出現MSE時，從頭開始播放。</p> <p>· 19049年：播放期間視訊遭封鎖時，Chrome、IE和Firefox上的Flash Player未報告錯誤狀態。</p> <p>· 17205:視訊播放會在播放未混音串流時停止數小時，而音訊仍繼續播放（Chromium期刊# 664033）。</p> <p>· 12308:指定composition_time_offset的DASH串流可能會在Chrome瀏覽器上套用timeStampOffset，導致負解碼時間，因此MEDIA_ERR_SRC_NOT_SUPPORTED錯誤（Chromium期刊#398141）。</p> <p>· 14126:由於MSE來源緩衝區中的內部間隙，Firefox（問題# 1316024）上的播放可能會停止。 嘗試搜尋以繼續播放。</p> <p>· 1915年：MS Edge和IE 11（Win 8.1和10）未在CORS重新導向時將原始碼設為null，但因為標題不是null而導致播放錯誤而失敗。</p> <p>· 19861：已播放媒體在來源緩衝區上附加行為的問題。 Chrome拒絕附加的片段，包括moov，造成後續的解碼錯誤。 （Chromium期號735335）</p> <p>19921年：某些HLS內容即使緩衝成功，仍會停止播放（Chromium問題#713540）</p> <p>· 20444：在IE和Edge上尋找緩衝範圍結束可能會導致播放停止。</p> <p>· 20511年：有時有廣告或沒有廣告時，HLS流會出現尋道拒絕。</p> <p>· 20743年：在Windows 10 Chrome上，HLS Live串流在MP4前滾播放前會播放數秒。</p> <p>· 21043:由於缺乏中繼資料，影片維度在初始載入時可能不正確。</p> <p>· 2115:如果播放清單中的視訊有前置廣告，則需要Android使用者手勢才能開始播放。</p> <p>· HLS Live不支援時間戳記變換。</p> <p>·不支援AAC-SSR音訊。</p> <p>不支援音訊轉碼器AC3和增強型AC3。</p> <p>·對於具有時間戳不連續但沒有不連續標籤的流</p> <p>·播放可能由於跳轉而出現錯誤和搜尋錯誤。</p> <p>·內容持續時間和播放持續時間可能不匹配。</p> <p>·表示法與轉譯之間的不連續性，應與其他方式相符，可能導致同步和停頓問題。</p> <p>·標題和WebVTT可能不會顯示在接近串流結尾的位置。</p> <p>·不支援跨時間戳記跳轉的音訊轉碼器變更。</p> <p>·不支援廣告插入。</p> <p>·快速轉發特技模式可能導致Win 8.1 IE 11上的播放回圈（MS問題#12446268）。</p> <p>破折號：</p> <p>·對於即時串流——支援動態類型的即時描述檔。</p> <p>·對於VoD串流——支援靜態類型的即時描述檔。</p> <p>針對VoD串流——不會針對廣告工作流程認證隨選設定檔。</p> </td> 
   <td><p>·不支援DASH Live和DASH Video on Demand串流。</p> <p>·全螢幕模式的iOS不支援PIP（畫中畫）視訊播放。</p> <p>在Safari（視訊標籤）擴充功能中，沒有正確內容類型標題的資訊清單較少無法運作。</p> </td> 
   <td><p>·傳送者應用程式中的應用程式ID必須與將「接收者」的URL註冊為「自訂接收者」應用程式時產生的ID相同。</p> <p>·參考播放器已通過DASH工作流程認證。 UI架構未通過認證。</p> <p>有關支援的媒體轉碼器清單，請參閱<a href="https://developers.google.com/cast/docs/media"><em>此處</em></a>。</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>一般播放（播放、暫停、搜尋）</td> 
   <td> </td> 
   <td>一八零九八年：在HLS LBA FER串流中觀察到某些尋道問題。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>可調式位元速率</td> 
   <td><p>· 20079:在緩衝範圍內的尋道時，緩衝區重寫。</p> <p>2008年：FlashABR行為與MSE一致。</p> </td> 
   <td><p>·由於緩衝區相關限制，ABR串流中的僅音訊備援變數會被忽略。</p> <p>· 12289:ABR控制參數不適用於未經過混合的HLS/DASH串流的音訊。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>608/708標題</td> 
   <td> </td> 
   <td><p>· 7810:在Android 4.4.4中，Chrome似乎不支援播放器使用的基本CSS字型系列，因此字型變更功能無法運作。</p> <p>·若有608個字幕，則無法變更CC頻道。</p> <p>· 608個標題不支援進階樣式功能。</p> <p>支援透過協助工具標籤發出訊號的內嵌標題(608/708)。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206:當播放器顯示標題時，會忽略WebVTT檔案中的區域標籤。</p> <p>·破折號：不支援分割的／分段的VTT檔案。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>資訊清單容錯</td> 
   <td>二一零五六年：使用Flash備援，如果主串流在播放期間傳回404錯誤，則即時串流不會發生容錯移轉。</td> 
   <td>資訊清單容錯功能僅適用於內容，不適用於廣告。</td> 
   <td>遺失的播放清單容錯功能僅適用於HTTP錯誤碼404的Safari。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>高級故障切換</td> 
   <td> </td> 
   <td><p>·區段容錯功能不支援略過無法使用的區段並持續播放。</p> <p>20533年：播放清單中遺失的區段應視為「不連續」，而應從下一個可用區段繼續播放。</p> <p>二一二六七年：由於故障切換而產生的串流切換可能導致下載舊區段。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>QoS和播放器通知</td> 
   <td>二一一二九年：在「Flash後援」的情況下，影格速率不可用。</td> 
   <td><p>· 11170:</p> <p>Timed_Event不適用於具有MSE的瀏覽器TVSDK，而瀏覽器TVSDK則不適用於具有Flash備援。</p> <p>二一一二九年：不會針對即時串流計算影格速率。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>支援Cookie標題</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials標幟和Cookie標題在Safari上不受支援。</p> <p>二一零五一年：若要在Safari中允許Cookie，請啟用「偏好設定&gt;隱私權」中的「Cookie和網站資料」設定。</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>自訂標籤</td> 
   <td>一四七六三年：不支援以#開頭的自訂標籤。 現在會在「Flash備援」期間建立並報告此類標籤的TimedMetadata物件。</td> 
   <td>無法認證帶內自訂標籤的串流。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>延遲裝訂音訊</td> 
   <td> </td> 
   <td><p>· HLS Live LBA串流不支援廣告插入。</p> <p>· 17273:HLS VOD LBA串流在發生故障切換時切換為預設轉譯，無法切換回上次選取的轉譯。</p> <p>· 20251:HLS Live LBA流可能會因搜索而停滯。</p> <p>· 20497:如果HLS LBA未混音串流的音訊或視訊影格接近串流結尾，則播放器會維持緩衝狀態。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302重新導向</td> 
   <td> </td> 
   <td><p>一五七八七年：302</p> <p>Windows Edge和IE瀏覽器不支援重新導向最佳化，因為這些瀏覽器不支援XMLHttpRequest物件中的responseURL屬性。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表17:進階播放功能**

<table> 
 <tbody> 
  <tr> 
   <td>內容類型</td> 
   <td>功能</td> 
   <td>Flash</td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>iOS Safari中的HTML5</strong></td> 
   <td><strong>Chromecast（僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>在偏移處播放</td> 
   <td><p>以特定偏移值開始播放不支援MP4內容。</p> </td> 
   <td>二零四九二年：在內容從偏移值繼續之前播放偏移之前的中間卷廣告。</td> 
   <td>iOS不支援使用偏移功能的播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>順暢的滴答功能不適用於沒有iFrame轉譯的串流。</td> 
   <td><p>· Firefox和Internet Explorer不支援特技播放調整功能，因此這些瀏覽器無法使用反向特技播放模式。</p> <p>·在播放內容與廣告時，不提供特技播放。</p> <p>· 10435:在DASH播放期間，Internet Explorer(Win 8.1)上的前向特技播放會凍結視訊</p> <p>間歇性。 這是因為我們使用視訊元素playbackRate屬性，而無特技播放調整。</p> <p>一四一八二年：有時，在Chrome瀏覽器倒轉期間，可能無法接收搜尋事件，因此特技模式無法運作。</p> <p>· 14942年：即使在非特技播放串流的情況下，您也可以在Android的Chrome上設定播放速率，但不會套用設定，而且播放仍會以正常速率進行。</p> <p>· 17308:在Trickplay模式下，搜尋不起作用。</p> <p>· 17309:在Chrome瀏覽器上，反向特技模式無法持續超過2秒。</p> <p>19272年：在DASH串流的情況下，特技播放可能無法從Windows 10 Edge瀏覽器的緩衝中恢復。</p> </td> 
   <td>不支援倒轉特技模式。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>ID3剖析</td> 
   <td>20346年：SDK也應傳回ID3影格的文字編碼位元組。</td> 
   <td><p>SDK會忽略音訊資料傳輸串流(ADTS)中可用的ID3標籤。</p> <p>· 12378:ID3計時中繼資料會在Flash和瀏覽器上以不同的時間進行剖析，並具有MSE支援，因此參考播放器時間軸上的顯示行為也不同。</p> <p>· 19247年：UI架構不支援ID3剖析。</p> </td> 
   <td><p>· 20323:Safari不會剖析用於傳送aac區段第一個範例時間戳記的PRIV ID3標籤（Safari問題#32422733）</p> <p>· 20350:在某些裝置（包括MAC OS X 10.1、iPad10）上，Safari在特技模式下不提供提示變更事件，因此未收到ID3影格。 （Safari問題#32450526）</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>不連續標籤支援</td> 
   <td> </td> 
   <td><p>·包含中斷的HLS串流不支援用戶端廣告插入。</p> <p>· HLS串流中不允許不連續的音訊轉碼器變更。</p> <p>·具有不連續標籤的HLS流不支援音頻軌道開關</p> </td> 
   <td>不連續序列號是HLS串流在Safari上播放時的必要條件。</td> 
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
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>iOS Safari中的HTML5</strong></td> 
   <td><strong>Chromecast（僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>AES-128加密內容不支援位元組範圍。</td> 
   <td>一二三二四年：如果未指定IV標籤，HLS AES-128加密串流無法在Safari上播放。</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660:HTML5播放器會針對過期的PlayReady加密破折號內容引發內部伺服器錯誤。</p> <p>· 16720:如果句點標籤中的start屬性缺失，則DASH DRM加密內容將無法運作。</p> <p>· 18589:使用Xlink的DRM保護虛線音訊VoD多時段串流不支援播放。</p> <p>· 18653:使用多鍵播放Widevine MultiPeriod內容時，會在第一個時段停止，且無法切換至下一個時段。</p> <p>· 18656年：可播放的多時段串流，使用不同的金鑰加密，無法播放。</p> <p>Playready 2.0 for Dash未取得認證。</p> <p> </p> <p> </p> </td> 
   <td>一二六零二年：HLS Fairplay DRM中繼資料會由Safari上的HTML5播放器重新整理</td> 
   <td><p>可播放透過Bento4封裝的DASH Widevine DRM內容。 透過Offline Packager和Shaka Packager封裝的內容不會播放。 不支援DASH PlayReady DRM。</p> </td> 
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
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>iOS Safari中的HTML5</strong></td> 
   <td><strong>Chromecast（僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>前／中/後</td> 
   <td> </td> 
   <td><p>·具有HLS即時內容的前置廣告以雙播放器模式播放。</p> <p>·不支援含HLS內容的DASH廣告和含DASH內容的HLS廣告。</p> <p>· 19002:在HTML5 Player中，具有MSE adBreak。 insertionType不返回正確值來描述正確的插入類型，即插入的客戶端和插入的伺服器。</p> <p>7794:在行動裝置（iOS、Android with Chrome 33或更低版本或原生瀏覽器）上，預設控制列以全螢幕模式顯示，搜尋列和快速前進按鈕在廣告播放時可用。</p> <p>· 11048:在使用媒體來源擴充功能時，從廣告切換至HLS Live內容並不順暢。</p> <p>· 16083:在Android 4.4 Chrome v52上，有時含HLS內容的HLS廣告會在停止播放後導致管道解碼錯誤。</p> <p>· 16097:未處理在廣告中斷期間遇到的錯誤，可能會導致主串流停止播放。</p> <p>· 18095:HLS即時內容不支援MP4廣告。</p> <p>19120年：對HLS廣告進行多次搜尋時，HLS內容可能會導致串流停止播放。</p> <p>· 19131年：從前段廣告插播切換為內容時，可能會出現緩衝覆蓋。</p> <p>· 20296:在HLS Live串流中，在DVR視窗中尋找，接著尋找已解析的中間卷，可能會導致播放停頓。</p> <p>· 20298:HLS Live串流中間卷在第一個中間卷時停止，並從DVR窗口移出。</p> <p>· 20317:當切換至下一個廣告或從廣告切換至內容時，HLS Live串流可能會停止，以防廣告插播包含多個廣告。</p> 
    <ul> 
     <li>HLS Live串流的DVR視窗中的廣告無法解決。</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK不符合VMAP回應中VAST adSource的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779年：SDK不會遵循VAST adSource的VMAP回應內的序列屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014年：不支援VMAP重複屬性。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>創意重新封裝</td> 
   <td> </td> 
   <td>二一四六四年：如果廣告插播中的其中一個廣告無法進行創意重新封裝，廣告回應會完全捨棄。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表20:進階Ad Insertion功能(CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>內容類型</strong></td> 
   <td><strong>功能</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>Firefox、IE、Chrome、Android Chrome中的HTML5</strong></td> 
   <td><strong>iOS Safari中的HTML5</strong></td> 
   <td><strong>Chromecast（僅限DASH播放）</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>僅限廣告</td> 
   <td> </td> 
   <td>20056年：播放器技術屬性不相關，因為它以主要內容為基礎，在「僅廣告」播放時，主要內容是空的</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>自訂廣告政策</td> 
   <td> </td> 
   <td><p>· MP4廣告和MP4內容不支援廣告行為。</p> <p>· 13973:自訂廣告行為- SKIP政策在與MSE搭配使用時不會擲回完整事件。</p> <p>· 14939年：自訂廣告行為原則略過和略過廣告插播不適用於DASH內容。</p> <p>· 17131:廣告的第一個畫格可見，然後內容在SKIP廣告中斷政策的情況下繼續。</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>配套廣告／橫幅廣告／可點選廣告</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>使用參考播放器時，橫幅廣告不可見。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· VPAID廣告不支援廣告行為。</p> <p>· 15032:不支援VPAID廣告與廣告中斷時的MP4或HLS廣告搭配使用。</p> <p>· 19001:在Android和iOS上，當VPAID廣告以MP4為主內容播放時，可聽到雙音軌、主要內容之一和廣告之一。</p> <p>· 20762:畫中畫(PIP)不支援VPAID廣告。</p> <p>· 21172:未收到包含VPAID廣告的HLS VOD內容的播放完整事件。</p> <p>· 21173:對於HLS VOD內容和後置卷VPAID廣告，未收到onAdBreakCompleteEvent。</p> </td> 
   <td>播放器在VPAID廣告和主內容之間切換時，在正常模式和全螢幕模式之間切換。</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**表21:整合**

| **內容類型** | **功能** | **Flash** | **Firefox、IE、Chrome、Android Chrome中的HTML5** | **iOS Safari中的HTML5** | **Chromecast（僅限DASH播放）** |
|---|---|---|---|---|---|
| VOD + Live | Adobe AnalyticsVHL整合 |  | 19004年：視訊分析追蹤無法透過UI設定器工具使用。 |  |  |

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。