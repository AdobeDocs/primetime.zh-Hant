---
title: Android適用的TVSDK 3.15發行說明
description: Android適用的TVSDK 3.15發行說明說明，說明TVSDK Android 3.15的新增或變更專案、已解決和已知問題以及裝置問題
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Android適用的TVSDK 3.15發行說明 {#tvsdk-for-android-release-notes}

Android適用的TVSDK 3.15發行說明說明，說明TVSDK Android 3.15的新增或變更專案、已解決和已知問題以及裝置問題。

Android參考播放器隨Android TVSDK包含在您的發佈的範例/目錄中。 隨附的README.md檔案說明如何建立參考播放器。

>[!NOTE]
>
>如發行版本隨附的README.md所述，若要成功建置參考播放器，請務必執行下列作業：
>
>1. 從下載VideoHeartbeat.jar [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) （Android v2.0.0適用的VideoHeartbeat資料庫）
>1. 將VideoHeartbeat.jar擷取至libs/資料夾。

相較於舊版，適用於Android的TVSDK提供許多效能改善專案。 除了支援多CDN外，提供高品質的觀看體驗，並具備1.4版的所有功能。

支援和不支援的完整功能集會顯示在 [功能對照表](#feature-matrix) 一節。

## Android TVSDK 3.15

此版本修正缺少創意標籤或應用程式當機多次的問題。 [!UICONTROL url CDATA] 在中是空的 [!UICONTROL VAST] 回應。

若要瞭解此版本及先前版本中的錯誤修正，請參閱 [Android版TVSDK中已修正的問題](#resolved-issueszd).

### 舊版版本中的新功能和增強功能

**Android TVSDK 3.14**

此版本修正以下情況時應用程式當機的問題： [!UICONTROL CDATA] 任何下列專案的節點為空： [!UICONTROL ClickTracking]， [!UICONTROL CustomClick] 或 [!UICONTROL CompanionClickTracking] VAST回應中的元素。

**Android TVSDK 3.13**

Widevine DRM串流在FireTV裝置上的ABR開關上凍結或顯示黑色框架，包括Fire TV第3代吊墜和Fire TV Cube第1代和第2代裝置。

若要解決此問題，請設定API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` 在起始播放之前，針對指定的Fire TV裝置。 預設值為false。

**Android TVSDK 3.12**

Primetime參考應用程式的Gradle版本已更新至5.6.4版。

若要使用Android Studio設定及執行參考應用程式，請依照TVSDK zip隨附的讀我檔案中的指示操作。 `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

目前版本中修正的主要客戶問題如下所述： [已解決問題](#resolved-issues) 區段。

**Android TVSDK 3.11**

* **允許擷取保護系統特定標頭(PSSH)方塊** - TVSDK可擷取與目前載入的媒體資源相關聯的保護系統專屬標題方塊。 新API `getPSSH()` 新增至 `com.adobe.mediacore.drm.DRMManager`.

如需詳細資訊，請參閱 [Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

此版本著重於修正中提及的主要客戶問題 [已解決問題](#resolved-issues) 區段。

**Android TVSDK 3.9**

* **透過HTTPS的安全傳遞** - Android TVSDK 3.9透過HTTPS推出安全傳送功能，以無與倫比的規模與效能安全傳送內容。

  為了透過HTTPS啟用安全傳送，在中引進了新API `NetworkConfiguration` 類別。

  `public void setForceHTTPS (boolean value)`

  `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **含部分廣告插播功能的前置滾動支援**  — 透過這項增強功能，TVSDK 3.8可支援具有部分廣告插播功能(PABI)的前段廣告。

會播放前段廣告（如果有的話），然後從即時點播放內容，模擬直播電視的體驗。

**Android TVSDK 3.7**

* 對於Widevine測試內容，為新的API `setMediaDrmCallback` DRManager類別中的會顯示以覆寫MediaDrmCallback介面的預設實作。

  `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 修正無法處理的AppCrash錯誤 `MediaPlayerEvent.ITEM_UPDATED` 在C++層（Android 64位元）中。

**Android TVSDK 3.6**

* **提升應用程式以符合64位元需求**  — 原生程式庫 `(libAVEAndroid.so)` 現已升級，並提供兩個版本。 現有的Armeabi （32位元）原生程式庫位置已從變更 `/framework/Player to /framework/Player/armeabi` 以及中引進了額外的arm64-v8a （64位元）程式庫 `/framework/Player/arm64-v8a.`

**版本3.5**

* **即時的廣告解析度** - TVSDK 3.5從時間軸移除對播放廣告的支援。

* **啟用離線播放支援**  — 透過離線播放，使用者現在可以將視訊內容下載到其裝置，並在未連線時觀看。 如需詳細資訊，請參閱&quot;[使用Android離線播放](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).」

**版本3.4**

* TVSDK現在支援CBC加密和純資料流的CMAF資料流播放。

**版本3.3**

* **API變更**

   * 新的API已新增至 `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` 處理網路錯誤和逾時。
      * 其中(n)是重試的次數。

**版本3.2**

* **平行廣告解析度和資訊清單下載支援**

   * TVSDK 3.2支援同步解析度，而非所有廣告請求和廣告插播（VMAP除外）的循序解析度。

   * 同時下載廣告插播中的所有廣告資訊清單。

* **啟用廣告解析和資訊清單下載逾時支援。**

   * 使用者現在可以為整體廣告解析度和資訊清單下載設定逾時值。  在VMAP中，逾時值適用於個別廣告插播，因為所有廣告插播會依序解析。

* **在AdvertisingMetadata類別中推出新API：**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **已從AdvertisingMetadata類別中移除下列API：**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **使用AC3/EAC3音訊轉碼器啟用串流播放**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 在 `MediaPlayer` 類別

* **TVSDK支援CMAF和加密的Widevine CTR的純資料流播放。**

* **現在支援播放4K HEVC資料流。**

* **平行廣告呼叫請求** - TVSDK現在會同時預先擷取20個廣告呼叫請求。

**版本3.0**

* **TVSDK 3.0支援高效率的視訊編碼(HEVC)資料流。**

* **即時 — 解決廣告更接近廣告標籤的問題**
延遲廣告解析現在會獨立解析每個廣告插播。 以前，廣告解析是兩階段方法：在播放開始前解析前段落，並在播放開始後合併所有中間/後段落。 透過此增強功能，每個廣告插播現在會在廣告提示點之前的特定時間解決。

>[!NOTE]
>
>延遲廣告解析現在已變更為預設關閉，並明確需要啟用。

新的API已新增至 `AdvertisingMetadata::setDelayAdLoadingTolerance` 以取得與此廣告中繼資料關聯的延遲廣告載入容錯。\
現在可在PREPARATION之後立即進行搜尋，在廣告插播上搜尋將會在搜尋完成之前立即解決問題。\
訊號模式 `SERVER_MAP` 和 `MANIFEST_CUES` 支援。

如需詳細資訊，請參閱 [Android適用的TVSDK 3.0程式設計師指南](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) API和事件變更的相關資訊。

* **已更新 `targetSdkVersion` 至最新版本**

已更新 `targetSdkVersion` 從19到27，順利運作。

* **Placement.Type getPlacementType()現在是介面TimelineMarker上的方法**

  此方法會傳回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL等版位型別。 如果廣告插播未解析，TimelineMarker介面上的getDuration()方法將會傳回0。

**版本2.5.6。**

* **TVSDK 2.5支援Android P。**

* **啟用背景音訊**

  若要在應用程式從前景移至背景時啟用音訊播放，應用程式應呼叫 `enableAudioPlaybackInBackground` 當播放器處於「已準備」狀態時，具有true作為引數的MediaPlayer的API。

* **MediaPlayer類別中的alwaysUseAudioOutputLatency（布林值）**

設定後，請在音訊時間戳記計算中使用輸出延遲。
布林值引數val - True會在音訊時間戳記計算中使用音訊輸出延遲。

* **最佳化，即使頻寬速度突然下降，也能提供最佳的播放體驗**

TVSDK現在會視需要取消進行中的區段下載，並動態切換至適當的轉譯。 這是透過順暢切換位元速率而不中斷來完成。

**版本2.5.5**

* **部分廣告插播插入**

  在廣告中加入，而不引發部分觀看廣告追蹤的電視式體驗。\
  範例：使用者在包含三個30秒廣告的90秒廣告插播中間（在40秒）加入。 這是插播中第二個廣告的10秒。

   * 第二個廣告會播放剩餘的持續時間（20秒），然後是第三個廣告。

   * 部分已播放廣告（第二個廣告）的廣告追蹤器不會觸發。 只會引發第三個廣告的追蹤器。

* **安全透過HTTPS載入廣告**

  Adobe Primetime提供可透過https要求第一次呼叫primetime廣告伺服器和CRS的選項。

* **新增至CRS請求的AdSystem和Creative ID**

  現在包含 `AdSystem` 和 `CreativeId` 做為1401和1403要求中的新引數。

* **NetworkConfiguration類別中的API setEncodeUrlForTracking已移除** 因為URL中的不安全字元應經過編碼。

**版本2.5.4**

Android TVSDK v2.5.4提供下列更新和API變更：

* 預設值的變更 `WebViewDebbuging`

  `WebViewDebbuging` 值設定為 `Fals`e依預設。 若要啟用，請呼叫 `setWebContentsDebuggingEnabled(true)` 在應用程式中。

* **OpenSSL和Curl版本升級**

  將libcurl更新至v7.57.0，並將OpenSSL更新至v1.0.2k。

* VAST回應物件的應用程式層級存取權

  推出新的API `NetworkAdInfo::getVastXml()` 可讓使用者存取應用程式的VAST回應物件。

**版本2.5.3**

Android TVSDK v2.5.3提供下列更新和API變更。

* 建議所有使用CRS的TVSDK客戶透過TVSDK 2.5.3.85或Android最新版本升級應用程式。 這是現有應用程式實作的替代方式。 TVSDK升級後，在Proxy工具（例如：Charles）中檢查CRS創意URL要求，並確認路徑中的主機名稱和版本反映為如以下範例URL結構中所示。

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的使用者代理程式可自訂：我們已新增一些新的API來自訂使用者代理。

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* 在Android應用程式和TVSDK之間共用Cookie： Android TVSDK現在支援在JAVA層（儲存在Android應用程式的CookieStore中）和C++ TVSDK層之間存取Cookie。 現在，您可以在原生C++圖層中，設定及/或修改Cookie，因為這些專案會公開至Java Cookie Store。

* API變更：

   * 新事件 `CookiesUpdatedEvent` 「 」已新增。 當媒體播放器的Cookie更新時，它就會被分派。

   * 新的API已新增至 `NetworkConfiguration::set/ getCustomUserAgent()` 以使用自訂使用者代理。

   * 新的API已新增至 `NetworkConfiguration::set/ getEncodedUrlForTracking` 以強制編碼不安全的字元。

   * 新的API已新增至 `NetworkConfiguration::getNetworkDownVerificationUrl()` 設定容錯移轉時的網路驗證URL。

   * 新屬性已新增至 `TextFormat::treatSpaceAsAlphaNum` 定義在顯示註解時，是否將空格視為英數字元。

* 中的變更 `SizeAvailableEvent`. 先前， `getHeight()` 和 `getWidth()` 方法 `SizeAvailableEvent` 在2.5.2中，用來傳回媒體格式所傳回的影格高度和影格寬度。 現在，它會分別傳回解碼器傳回的輸出高度和輸出寬度。

* 緩衝行為的變更：緩衝行為已變更。 由應用程式開發人員自行決定緩衝區為空時該怎麼做。 2.5.3在緩衝區空白的情況下使用播放緩衝區大小。

**版本2.5.2**

Android TVSDK v2.5.2提供重要的錯誤修正和一些API變更。

**版本2.5.1**

Android 2.5.1版的重要新功能。

* **效能改良 —** 新的TVSDK 2.5.1架構提供多項效能改善專案。 根據第三方基準測試的統計資料，新架構的啟動時間比業界平均減少5倍，掉格減少3.8倍：

* **立即開啟VOD和即時 —** 當您啟用立即開啟時，TVSDK會在播放開始之前初始化並緩衝媒體。 因為您可以在背景同時啟動多個MediaPlayerItemLoader執行個體，所以您可以緩衝多個串流。 當使用者變更頻道，並且串流已正確緩衝時，新頻道上的播放立即開始。 TVSDK 2.5.1也支援以下專案的立即開啟： **即時** 串流也會。 即時視窗移動時會重新緩衝即時資料流。

* **改善ABR邏輯 —** 新的ABR邏輯是以緩衝區長度、緩衝區長度變更速率，以及測量的頻寬為基礎。 這可確保ABR在頻寬波動時選擇正確的位元速率，並透過監控緩衝區長度變更的速率，最佳化位元速率切換的實際發生次數。

* **部分割槽段下載/細分 —** TVSDK進一步縮小每個片段的大小，以儘快開始播放。 ts片段必須每兩秒有一個關鍵影格。

* **延遲廣告解析度 —** TVSDK不會等到非前段廣告解析後才開始播放，因此縮短了啟動時間。 除非解決所有廣告，否則仍不允許搜尋和特技播放等API。 這適用於搭配CSAI使用的VOD資料流。 在廣告解析完成前，不允許執行搜尋和快轉等作業。 對於即時資料流，此功能無法在即時活動期間啟用廣告解析功能。

* **持續性網路連線 —** 此功能可讓TVSDK建立並儲存持續性網路連線的內部清單。 這些連線會重複用於多個要求，而不是為每個網路要求開啟新的連線，然後在之後將其銷毀。 這會提高網路程式碼的效率並縮短延遲時間，進而加快播放效能。
TVSDK開啟連線時，會要求伺服器輸入 *保持連線* 連線。 有些伺服器可能不支援這種連線型別，在這種情況下TVSDK會退回以針對每個請求再次建立連線。 此外，雖然持續連線預設為開啟，但TVSDK現在提供設定選項，讓應用程式可視需要關閉持續連線。

* **平行下載 —** 同時下載視訊與音訊而非串列下載，可減少啟動延遲。 此功能可播放HLS Live和VOD檔案、最佳化伺服器的可用頻寬使用量、降低進入緩衝區執行不足狀況的可能性，以及將下載和播放之間的延遲降至最低。

* **平行廣告下載 —** TVSDK會在點選廣告插播之前預先擷取與內容播放並行的廣告，因此可順暢地播放廣告和內容。

* **播放**

* **MP4內容播放 —** MP4短片不需要重新轉碼，就能在TVSDK中播放。

  >[!NOTE]
  >
  >MP4播放不支援ABR切換、特技播放、廣告插入、延遲音訊繫結和子細分。

* **以最適化位元速率(ABR)進行特技播放 —** 此功能可讓TVSDK在特技播放模式中切換iFrame串流。 您可以使用非iFrame設定檔，以較低速度進行特技播放。

* **更流暢的魔術遊戲 —** 這些改善專案可增強使用者體驗：

   * 根據頻寬和緩衝區設定檔，在特技播放期間選擇最適化位元速率和影格速率

   * 使用主串流而不是IDR串流，以取得最高30 fps的快速播放。

* **內容保護**

   * **以解析度為基礎的輸出保護 —** 此功能將播放限制繫結至特定解析度，提供更精細的DRM控制項。

* **工作流程支援**

   * **直接帳單整合 —** 這會將計費量度傳送至Adobe Analytics後端，後者會由Adobe Primetime針對客戶使用的資料流進行認證。

  TVSDK會根據客戶銷售合約自動收集量度，以產生開立帳單所需的定期使用報表。 在每個資料流開始事件上，TVSDK會使用Adobe Analytics資料插入API將計費量度（例如內容型別、廣告插入啟用旗標，以及drm啟用旗標）根據計費資料流的持續時間傳送至Adobe Analytics Primetime擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 系統會根據要求定期傳送此計費使用報告給客戶。 這是計費功能的第一個階段，僅支援使用計費。 您可以使用本檔案中說明的API，根據銷售合約進行設定。 此功能預設為啟用。 若要關閉此功能，請參閱參考播放器範例。

   * **改善容錯移轉支援 —** 即使主機伺服器、播放清單檔案和區段失敗，仍實施其他策略以繼續不間斷播放。

* **Advertising**

   * **Moat整合 —** 支援來自Moat的廣告可見度測量。

   * **隨附橫幅 —** 隨附橫幅會與線性廣告一併顯示，且通常在廣告結束後繼續顯示在檢視上。 這些橫幅可以是html型別(HTML片段)或型別iframe （iframe頁面的URL）。

* **Analytics**

   * **VHL 2.0 -** 這是最新最佳化的視訊心率程式庫(VHL)整合，可自動收集Adobe Analytics的使用資料。 API的複雜度已降低，以簡化實作。 下載VHL資料庫 [Android適用的v2.0.0](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) 並解壓縮libs資料夾中的JAR檔案。

* **SizeAvaliableEventListener**

   * `getHeight()` 和 `getWidth()` 方法 `SizeAvailableEvent` 現在會分別傳回高度和寬度的輸出。 顯示外觀比例的計算方式如下：

     ```java
     SizeAvailableEvent e;
     DAR = e.getWidth()/ e.getHeight();
     ```

     以Sar寬度和Sar高度表示的儲存外觀比例也可用來計算影格寬度和影格高度：

     ```java
     SAR = e.getSarWidth()/e.getSarHeight();
     frameHeight = e.getHeight();
     frameWidth = e.getWidth()/SAR;
     ```

* **Cookie**

   * Android TVSDK現在支援存取Android應用程式CookieStore中儲存的JAVA Cookie。 每當新的Cookie成為的一部分時，就會提供回呼API (onCookiesUpdated)來記錄 **Set-Cookie** 回應標頭。 透過CookieStore在特定URI/網域上設定這些Cookie值，可將這些Cookie用為用於不同URI/網域的HttpCookie清單。 同樣地，TVSDK中的Cookie值也是使用CookieStore新增API來更新。

## 功能矩陣 {#feature-matrix}

適用於Android的TVSDK支援許多您可實作的功能，以將功能新增至視訊應用程式。

在下列功能表中，「Y」表示目前版本支援該功能。

| 功能 | 內容型別 | HLS |
|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD +即時 | Y |
| FER — 一般播放（播放、暫停、搜尋） | FER VOD | Y |
| 在廣告播放時搜尋 | VOD +即時 | 不支援 |
| HEVC播放 | VOD +即時 | 僅限fMP4容器 |
| AC3和EAC3 | VOD +即時 | 不支援 |
| MP3 | VOD | 不支援 |
| MP4內容播放 | VOD | Y |
| 最適化位元速率切換邏輯 | VOD +即時 | Y |
| 僅限音訊的播放 | VOD +即時 | Y |
| 多CDN支援 | VOD +即時 | 不支援 |
| 使用純音訊媒體播放廣告 | VOD +即時 | 不支援 |
| 隱藏式字幕 — 608/708 | VOD +即時 | Y |
| 隱藏式字幕 — WebVTT | VOD +即時 | Y |
| 資訊清單容錯移轉 | VOD +即時 | Y |
| 進階容錯移轉 | VOD +即時 | Y |
| QoS和播放器通知 | VOD +即時 | Y |
| 支援Cookie標頭 | VOD +即時 | Y |
| 支援自訂HTTP標頭 | VOD +即時 | Y （需要允許清單） |
| 設定緩衝區控制引數 | VOD +即時 | Y |
| 設定最適化位元速率控制 | VOD +即時 | Y |
| 自訂資訊清單標籤 | VOD +即時 | Y |
| 延遲音訊繫結 | VOD +即時 | Y |
| 302重新導向 | VOD +即時 | Y |
| 有位移的播放 | VOD +即時 | Y |
| 特技播放 | VOD +即時 | Y |
| 特技遊戲中的慢動作 | VOD +即時 | 不支援 |
| Smooth Trick Play （含ABR） | VOD +即時 | Y |
| ID3剖析 | VOD +即時 | Y |
| 廣告中斷 | VOD +即時 | 不支援 |
| 立即開啟 | VOD +即時 | 不支援 |
| 支援不連續標籤 | VOD +即時 | Y |
| 302重新導向粘著度 | VOD +即時 | Y |

| 功能 | 內容型別 | HLS |
|---|---|---|
| 一般播放，啟用廣告 | VOD +即時 | Y |
| 已啟用廣告的FER內容 | VOD | Y |
| 預設廣告行為 | VOD +即時 | Y |
| VAST 2.0/3.0 | VOD +即時 | Y |
| VMAP 1.0 | VOD +即時 | Y |
| MP4廣告 | VOD +即時 | Y （來自CRS） |
| 啟用廣告的Trick Play | VOD +即時 | Y |
| 僅限廣告 | VOD | Y |
| 目標定位引數 | VOD +即時 | Y |
| 自訂引數 | VOD +即時 | Y |
| 自訂廣告行為 | VOD +即時 | Y |
| 自訂廣告標籤 | 即時 | Y |
| 自訂廣告解析程式 | VOD +即時 | Y |
| Freewheel自訂廣告解析程式 | VOD | Y |
| C3 | VOD +即時 | 不支援 |
| 延遲廣告解析 | VOD | Y |
| 不連續標籤支援 — SSAI | VOD +即時 | Y |
| 隨附廣告、橫幅廣告和可點按廣告 | VOD +即時 | Y |
| VPAID 2.0 | VOD +即時 | Y (JS) |
| 早期廣告結束 | 即時 | Y |
| 規則型創意優先順序 | VOD +即時 | Y |
| CRS規則 | VOD +即時 | Y |
| JSON Ad Resolver | VOD +即時 | 不支援 |
| Moat整合 | VOD +即時 | Y |
| 部分廣告插播插入 | 即時 | Y |

| 功能 | 內容型別 | HLS |
|---|---|---|
| AES加密 | VOD +即時 | Y |
| AES加密範例 | VOD +即時 | Y |
| 代碼化的資料流 | VOD +即時 | Y |
| Widevine DRM | VOD +即時 | 僅限fMP4容器 |
| Primetime DRM | VOD +即時 | Y |
| 外部播放(RBOP) | VOD +即時 | 僅限Primetime DRM |
| 授權輪換 | VOD +即時 | 僅限Primetime DRM |
| 金鑰輪換 | VOD +即時 | 僅限Primetime DRM |

| 功能 | 內容型別 | HLS |
|---|---|---|
| Adobe Analytics VHL整合 | VOD +即時 | Y |
| 帳單 | VOD +即時 | Y |

## 已解決問題 {#resolved-issues}

如果解決方法與報告的問題相關，則會顯示Zendesk參考，例如ZD#xxxxx。

**Android TVSDK 3.15**

本節提供TVSDK 3.14 Android版本中已解決之問題的摘要。

* ZD#46903 — 遺失創意標籤或發生下列情況時，應用程式當機多次 [!UICONTROL url CDATA] 在中是空的 [!UICONTROL VAST] 回應。

**Android TVSDK 3.14**

* ZD#46903 — 應用程式當機 [!UICONTROL CDATA] 任何下列專案的節點為空： [!UICONTROL ClickTracking]， [!UICONTROL CustomClick] 或 [!UICONTROL CompanionClickTracking] 中的元素 [!UICONTROL VAST] 回應。

### 舊版中的已解決問題

**Android TVSDK 3.12**

* ZD#40584 - Primetime參考應用程式未使用最新Gradle版本建置。

**Android TVSDK 3.11**

* ZD#41252 - WebVTT中的韓文字元在Android 7.1之後中斷。

**Android TVSDK 3.10**

* ZD#40340 — 在封鎖列出所有TS (TypeScript)檔案後，應用程式在嘗試播放時當機並出現「應用程式未回應」錯誤。

**Android TVSDK 3.8**

* 未新增任何新問題。

**Android TVSDK 3.7**

* 未新增任何新問題。

**Android TVSDK 3.6**

* 未新增任何新問題。

**版本3.5**

* ZD#37503 — 系統會快取CRS規則的JSON回應，以避免重複請求。

**版本3.4**

* ZD#37996 — 修正線性和VOD CMAF HEVC資料流的播放斷斷續續的問題。
* ZD#37706 — 修正亂碼字幕的問題。
* ZD#37622 — 修正特定廣告的嚴重URISyntaxErrors問題。
* ZD#36938 — 修正位元速率切換至中間位元速率，然後在退出特技表演後恢復至最高位元速率的問題。

**版本3.3**

* ZD#37394 - CMAF資產快速前進會在速度變更後造成人工因素。
   * 修正特技播放期間設定檔變更所發生的問題。
* ZD#37396 — 某些中段和後段缺少廣告追蹤事件。
   * 已修正廣告追蹤事件的特定案例。
* ZD#37491 — 沒有包含錯誤中繼資料的HTTP狀態代碼。
   * 已處理在棧疊中較高位置傳播網路錯誤。
* ZD#37808 — 允許列出新的自訂標頭。
   * 此修正新增了SSAI_TAG支援。
* ZD#37622 — 來自特定Ad Pod的URISyntax錯誤。
   * 修正當客戶Android應用程式收到包含未編碼%的廣告時，串流播放當機的問題
* ZD#37631 - Android TVSDK的主要資訊清單重試機制。
   * 已在網路設定中新增處理此增強功能的API。 如果未使用此API，則不會重試資訊清單。 如果使用，則會重試資訊清單，以處理網路錯誤和逾時。

**版本3.2**

* ZD#37493 — 不會為序列中的第一個廣告間歇性地觸發即時播放的追蹤信標。
* ZD#36985- VMAP回應中未針對空白廣告插播傳送追蹤信標。
* ZD#37134 - TVSDK會間歇性地擲回VMAP回應的錯誤ID。

**版本3.0**

* ZD#33740 — 建立MediaPlayer物件並呼叫replaceCurrentResource()後，TVSDK會擲回不需要的警告

   * 改善先前的修正，只在播放器處於暫停狀態時呼叫還原

* ZD#36442 — 每次新播放都會中斷遠端偵錯工作階段的連線，導致無法偵錯。

   * Web檢視預設無法偵錯，因為預設不會啟用偵錯。 應用程式應視需要對從MediaPlayer.getCustomAdView()傳回的物件呼叫setWebContentsDebuggingEnabled(true)來啟用偵錯。

* ZD#33688 — 支援及時廣告解決

   * 廣告插播會依廣告插播位置之前的指定間隔來解析。

* ZD#36441 — 即時視窗持續時間持續增加超過5分鐘，導致多個問題。

   * 修正在計算虛擬即時點時，新增virtualStartTime兩次，導致此問題的問題。

**Android TVSDK 2.5.6**

* ZD #34992 — 隱藏式字幕中的語言是空的。

   * 修正TVSDK未從主要資訊清單剖析#EXT-X-MEDIA：TYPE=CLOSED-CAPTIONS以取得標題追蹤詳細資訊的情況。

* ZD #35078 - Android P驗證。

   * TVSDK 2..5.6已透過最新Android P測試版組建驗證。 新Android作業系統未發現任何問題。

* ZD #34149 — 即使發生錯誤，播放器仍會繼續要求資訊清單。

   * 修正TVSDK進行重複呼叫的情況，即使所有設定檔都已關閉（404錯誤）。

* ZD #31533 — 在應用程式傳送至背景後，在Android上播放音訊。

   * 已新增 `enableAudioPlaybackInBackground` MediaPlayer的API，此應用程式以「True」作為引數（當播放器處於「已準備」狀態時）進行呼叫，以在應用程式於背景時啟用音訊播放。

**Android TVSDK 2.5.5**

* ZD #21647 — 實際視訊大小為640x360時，Android TVSDK會通知640x368。

   * 因為變數m_nOutputHeight （在AndroidMCVideoDecoder內）會以影格高度而非實際輸出高度更新。 在函式getVideoFrame中進行相關變更，以正確計算m_nOutputHeight。

* ZD #26614 — 緊急 — 第三方廣告服務/程式化 — 無法提供曝光數。

   * 透過處理XML剖析中的案例，加強先前的修正，其中當&quot;space&quot;在&quot;equal&quot;符號之前，例如 &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android：將AdSystem和Creative ID新增至CRS請求。

   * 現在包含&#39;AdSystem&#39;和&#39;CreativeId&#39;作為新引數，出現在1401和1403請求中。

* ZD #33062 - TVSDK在CDATA節點下的VAST回應中發生垂直號字元時當機

   * NetworkConfiguration類別中的API setEncodeUrlForTracking已移除，成為要編碼之URL中的不安全字元

* ZD #33063 - CRS檔案選擇邏輯損毀 — TVSDK未傳送Webm格式的CRS要求，而是改為傳送3gpp檔案的要求。

   * 現在已修正邏輯。 在使用具有webm和3gpp格式的媒體檔案時，會針對webm傳送CRS請求。 而在同時使用採用3gpp格式的媒體檔案時，系統會針對最高位元速率的3gpp檔案傳送CRS要求。

* ZD #33125 - Android應用程式當機，且VMAP中有特定的DoubleClick標籤。

   * 修正此情況以避免當機。

* ZD #32256 — 授權輪換與金鑰輪換問題 — Adobe存取

   * 修正SampleAES內容使用DRM中繼資料進行區段初始化的問題。 適用於AES128內容。

* ZD #33619 — 快速轉送成長中的播放清單內容，這些內容在即時點附近停滯在緩衝狀態。

   * 處理在特技播放模式中跨過即時點時的情況

* ZD #34151 - TimedMetadata物件順序錯誤。

   * 兩個TimedMetadata事件如果屬於時間軸中的同一時間，則會以隨機順序出現。 維持其資訊清單中的原始順序。

* ZD #34189 — 嘗試開始廣告插播時發生問題。

   * 該問題與SSAI廣告有關，其使用不連續性進行拼接。 原因是當我們尋找這類廣告的開頭時，我們尋找關鍵影格，卻找不到它。 原因是廣告的最小音訊時間戳記在最小視訊時間戳記之前。 因此，我們最終會在錯誤的fragmentDump資料中搜尋關鍵影格。 現已修正。

* ZD #34528 — 在FireTV第3代硬體鎖上，視訊解析度無法升級至640x360以上。

   * 增強修正功能，加入最新的韌體更新

* ZD #34793 - TVSDK 2.5.x過去會在VideoEngine假設auditudeSettings可用但無法使用時，在某些情況下與自訂內容解析程式當機。

   * 當機的發生是因為Null共用指標(auditudeSettings)上的函式呼叫。 在VideoEngineTimeline：：placeToSourceTimeline()中新增條件檢查，以確保在呼叫該物件上的任何內容之前，auditudeSettings都可供使用。

* ZD #32584 — 無法存取 &lt;extensions> vast回應的節點。

   * 已修正有關XML剖析的問題，現在NetworkAdInfo提供 &lt;extensions> 節點

* ZD #35086 — 若是特定VMAP回應，無法從播放器取得完整的擴充功能資料。

   * 問題是擴充功能xml所特有的，因為如果擴充功能xml在屬性值內有雙引號，XML剖析將無法運作。 已修正問題。

**Android TVSDK 2.5.4**

* ZenDesk#33659 — 啟用Webview遠端偵錯的播放工作階段。

WebViewDebugging預設為False。 若要啟用偵錯，請使用setWebContentsDebuggingEnabled(true)，透過應用程式設定為true。

* ZenDesk#33011 — 如果CRS請求失敗，廣告時間軸未解析。

  當對廣告的CRS請求失敗時，時間軸會解析並播放其餘廣告。

* ZenDesk#34528 — 在FireTV第三代硬體鎖上，視訊解析度無法升級至640x360以上。

  視訊解析度會隨著位元速率切換而提高。

* ZenDesk#33192 — 透過AudioUpdatedEventListener：：onAudioUpdated擷取曲目時，AudioTrack的名稱為Null。

  在FireTV Stick的少數案例中，在沒有實際音訊更新時會引發onAudioUpdate事件。 此問題現在已修正。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自訂標籤訂閱無法運作。

  我們將ID3資料以位元組陣列（以支援APIC或一般資料）傳回給使用者端，而傳回1.4字串中的資料。 位元組陣列本身不處理Null結尾的字元，因此對使用者端顯示特殊字元。 此問題已立即修正。
* Zendesk#32670 — 播放器未容錯移轉至備援播放清單

  現在這項功能正常運作，setNetworkDownVerificationUrl也如預期般運作。
* Zendesk#32369 — 隱藏式字幕顯示不同的色彩記憶體或成品。

  已在最新組建中修正CC問題
* Zendesk#25590 — 增強功能：TVSDK Cookie存放區( C++至JAVA )

  Android TVSDK現在支援在JAVA層（儲存在Android應用程式的CookieStore中）與C++ TVSDK層之間存取Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎沒有PTPLAY-20269的修正

  此問題已修正並整合至2.5.2分支。
* Zendesk#31806 — 準備中的Auditude棒

  播放器卡在準備狀態，因為回應xml有空白標籤。 問題已修正。
* Zendesk#31727 - TVSDK 2.5隱藏式字幕字元已捨棄或拼寫錯誤。

  問題已修正，且我們不會捨棄/拼錯任何字元。
* Zendesk#31485 - DrmManager 2.5版

  透過新的DrmManager（前後關聯環境）建立DrmManager時發生一些問題。 實作提供DRMManager的DRMService類別。
* Zendesk#32794- 1080P解析度資料流無法在Android上播放

  我們變更了SizeAvailableEvent 2.5中的getHeight()和getWidth()方法，這些方法用於傳回媒體格式傳回的影格高度和影格寬度。 現在會分別傳回解碼器傳回的輸出高度和輸出寬度。
* Zendesk #19359Flash Player會因為#EXT-X-FAXS-CM屬性在設定層級資訊清單中的位置而當機。

  在個別位元速率或區段出現在播放清單之前，#EXT-X-FAXS-CM標籤必須一律出現在最上層播放清單中。

**Android TVSDK 2.5.2**

* Zendesk#17305隱藏式字幕中的不透明背景。

  TextFormat中的setTreatSpaceAsAlphaNum屬性會公開。 依預設，屬性為False。 在使用者端中將屬性設定為True以解決深色空格問題。

* Zendesk#25097 CC顯示具有包含CC設定的視覺成品。

  TextFormat中的setTreatSpaceAsAlphaNum屬性會公開。 依預設，屬性為False。 在使用者端中將屬性設定為True以解決深色空格問題。

* 傳出TVSDK播放器的Zendesk #31620使用者代理字串被截斷。

  128個字元後，使用者代理字串將不再被截斷。

  Adobe Primetime版本字串已新增至系統使用者代理。

* Zendesk #30809遺失SEEK_END事件會使應用程式無法轉換為播放狀態。
* 與舊版Primetime TVSDK相比，Zendesk #30415隱藏式字幕的「青色」顏色現在變成較暗的藍色（藍綠色）。

  顏色從深青色變更為青色。

* 未下載/解析Zendesk #30727 VOD廣告。

  在VMAP XML中，如果空白VAST標籤沒有明確的結尾標籤(&#39;&lt;/vast>&#39;)，且後面沒有新行字元，則VMAP XML無法正確剖析，廣告可能無法播放。

**Android TVSDK 2.5.1**

* 裝置特定(Samsung Galaxy Tab 4)當機；具有Auditude和點選廣告的VOD DRM LBA。
* VHL — 從位移開始內容時，會傳送不正確的心率呼叫。
* 播放VPAID廣告時，VHL心率會呼叫事件:type:播放廣告遺失。
* 在進入「完成」狀態後，播放器會針對後段廣告返回到「正在播放」狀態並顯示SKIP adBreakPolicy 。
* Cookie未附加至傳出廣告回呼。
* 廣告提示點不可見。
* 無法載入具有獨立EAC3 SAP追蹤的HLS。
* 媒體播放器還原後，TVSDK收到Screen On意圖導致播放器當機。

## 已知問題和限制 {#known-issues-and-limitations}

**Android TVSDK 3.11**

* 未新增任何新限制。

### 舊版中的已知問題和限制

**Android TVSDK 3.10**

* 未新增任何新限制。

**Android TVSDK 3.8**

* 未新增任何新限制。

**Android TVSDK 3.7**

* 未新增任何新限制。

**Android TVSDK 3.6**

* 未新增任何新限制。

**Android TVSDK 3.5**

* 未新增任何新限制。

**Android TVSDK 3.4**

* 尚未驗證CMAF (CBC)資料流的ID3、隱藏式字幕、延遲繫結音訊支援。
* 在某些裝置上，由於在CMAF串流的特技播放期間視訊扭曲可能出現在頂端，因此存在可重複性低的問題。

**Android TVSDK 3.3**

* CMAF資料流播放不支援clcp：c608字幕。

**Android TVSDK 3.2**

* TVSDK 3.2不支援CMAF範例AES和AES128資料流播放。
* HEVC CMAF資料流不支援隱藏式字幕播放。
* 圍繞非加密區段執行搜尋時，WV加密資料流會顯示綠色色彩。
* CMAF資料流不支援ID3事件。
* HLS資料流不支援TTML註解格式。

**Android TVSDK 3.0**

* 在這個版本中，HEVC支援有下列限制

   * 不支援DRM
   * CC (CEA 608/708)支援未驗證
   * 尚未提供4K支援
   * 未驗證ID3標籤支援

* 對於廣告進度事件，時間軸列可能無法反映100%正確的廣告播放時間。 作為因應措施，您可以使用 `adcompleteevent` 瞭解廣告播放完成和更新UI的各種用途，例如更新時間軸列、移除廣告相關UI等。
* 從VMAP傳回的大量廣告呼叫不接受即時Lookahead位置。

**Android TVSDK 2.5.6**

* 不支援同時有多個VMAP廣告插播。

**Android TVSDK 2.5.3**

此版本有以下問題：

* 即時視訊播放在低端裝置或不良網路狀況下可能有音訊 — 視訊同步問題。
* 對於FER資料流，virtualTime和localTime可能會不同。 此外，具有位移的FER無法運作。
* 搜尋延遲繫結音訊內容時，播放可能會卡住。
* LIVE內容的webVTT註解可能會間歇性地失去同步。
* 在結束廣告插播後，可以看到間歇性的快速播放少數影格。
* 有時候，即使播放了廣告，三元組包裝函式廣告插播也會擲回303錯誤。

**Android TVSDK 2.5.2**

此版本有以下問題：

* 低端裝置上的即時視訊播放可能有音訊 — 視訊同步問題。
* 搜尋至VOD媒體結尾時，播放可能會有時停止。
* 對於FER資料流，virtualTime和localTime可能會不同。 此外，具有位移的FER無法運作。

**Android TVSDK 2.5.1**

此版本的TVSDK有下列問題：

* 低端裝置上的即時視訊播放可能有音訊 — 視訊同步問題。
* 對於FER資料流，virtualTime和localTime可能會不同。 此外，具有位移的FER無法運作。
* 在VMAP XML中，如果存在沒有明確結尾標籤的空白VAST標籤(&lt;/vast>)，且後面沒有新行，則VMAP XML無法正確剖析，且廣告可能無法播放。
* 不支援VPAID後置滾動。

## 實用資源 {#helpful-resources}

* [系統需求](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Android適用的TVSDK 3.10程式設計師指南](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [API適用的TVSDK Android Javadoc參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API檔案](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html)  — 每個Java類別都有對應的C++類別，且C++檔案包含的說明資料比Javadocs更多，因此請參閱C++檔案以深入瞭解Java API。
* [TVSDK 1.4至2.5 for Android (Java)移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 如需處理熒幕開啟/關閉的情況，請參閱 `Application_Changes_for_Screen_On_Off.pdf` 組建中包含的檔案。
* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
