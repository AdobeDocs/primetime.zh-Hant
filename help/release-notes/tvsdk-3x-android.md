---
title: TVSDK 3.13 for Android版本注意事項
description: TVSDK 3.13 for Android發行說明說明TVSDK Android 3.13中的新增或變更內容、已解決和已知問題以及裝置問題
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5443'
ht-degree: 0%

---


# TVSDK 3.13 for Android發行說明{#tvsdk-for-android-release-notes}

TVSDK 3.13 for Android發行說明說明TVSDK Android 3.13中的新增或變更、已解決和已知問題以及裝置問題。

Android參考播放器隨附於Android TVSDK，位於您散發的範例／目錄中。 隨附的README.md檔案說明如何建立參考播放器。

>[!NOTE]
>
>要按照隨發行版分發的README.md中所述成功構建參考播放器，請確保執行以下操作：
>
>1. 從[https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)（Android v2.0.0的VideoHeartbeat程式庫）下載VideoHeartbeat.jar
>1. 將VideoHeartbeat.jar解壓縮至libs/資料夾。


適用於Android的TVSDK提供許多舊版的效能改進。 除了Multi-CDN支援外，它提供高品質的檢視體驗並具備1.4版的所有功能。

發行說明的[功能矩陣](#feature-matrix)一節中列出了完整的支援與不支援功能集。

## Android TVSDK 3.13

Widevine DRM串流會凍結FireTV裝置上ABR開關的黑色影格，包括Fire TV第3代墜飾和Fire TV Cube第1代和第2代裝置。

若要解決此問題，請在開始播放之前，先針對指定的Fire TV裝置設定API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`。 預設值為false。

### 舊版的新功能和增強功能

## Android TVSDK 3.12

Primetime Reference應用程式的圖檔版本現已更新為5.6.4版。

若要使用Android Studio來設定及執行參考應用程式，請依照TVSDK zip(`TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`)中提供的讀我檔案指示進行。

在[已解決的問題](#resolved-issues)一節中，會提及目前版本中修正的主要客戶問題。

**Android TVSDK 3.11**

* **允許獲取保護系統特定報頭(PSSH)框** - TVSDK允許獲取與當前載入的媒體資源相關聯的保護系統特定報頭框。新增至`com.adobe.mediacore.drm.DRMManager`的新API `getPSSH()`。

如需詳細資訊，請參閱「Widevine DRM」(Widevine DRM)。[](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md)

**Android TVSDK 3.10**

本版本著重於解決[已解決的問題](#resolved-issues)一節中提及的主要客戶問題。

**Android TVSDK 3.9**

* **透過HTTPS**  - Android TVSDK 3.9的安全傳送——透過HTTPS提供安全傳送功能，以無人能及的規模和效能安全地傳送內容。

   若要透過HTTPS進行安全傳送，`NetworkConfiguration`類別中引進了新的API。

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **具有部分廣告插播功能的前段廣告支援** -透過此增強功能，TVSDK 3.8支援具有部分廣告插播功能(PABI)的前段廣告。

播放前段廣告（如果有的話），然後內容從即時點播放，以模擬即時電視的體驗。

**Android TVSDK 3.7**

* 對於Widevine測試內容，會公開DRMManager類別中的新API `setMediaDrmCallback`以覆寫MediaDrmCallback介面的預設實作。

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 修正C++圖層（Android 64位元）中未處理`MediaPlayerEvent.ITEM_UPDATED`的AppCrash錯誤。

**Android TVSDK 3.6**

* **增強您的應用程式以符合64位元需求** -原生程式庫 `(libAVEAndroid.so)` 現已升級並提供兩種版本。現有的armeabi（32位元）原生程式庫位置已從`/framework/Player to /framework/Player/armeabi`變更，並在`/framework/Player/arm64-v8a.`中新增額外的arm64-v8a（64位元）程式庫

**第3.5版**

* **Just In Time Ad Resolution**  - TVSDK 3.5從時間軸移除對播放廣告的支援。

* **已啟用離線播放支援** -使用離線播放，使用者現在可以下載視訊內容至其裝置，並在未連線時觀看。如需詳細資訊，請參閱「[Offline Playback with Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)」。

**第3.4版**

* TVSDK現在支援CMAF串流播放，以播放CBC加密和純串流。

**第3.3版**

* **API變更**

   * 新增API至`NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*`以處理網路錯誤和逾時。
      * 其中(n)是重試次數。

**第3.2版**

* **平行廣告解析度與資訊清單下載支援**

   * TVSDK 3.2支援同步解析度，而非依序解析度，以處理除VMAP以外的所有廣告要求和廣告中斷。

   * 廣告分段中的所有廣告資訊清單都會同時下載。

* **已啟用廣告解析度和資訊清單下載逾時支援。**

   * 使用者現在可以設定整體廣告解析度和資訊清單下載的逾時值。  在VMAP中，逾時值會套用至個別廣告插播，因為所有廣告插播都會依序解決。

* **在AdvertisingMetadata類別中引入新的API:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **從AdvertisingMetadata類別的API下方移除：**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **使用AC3/EAC3音訊轉碼器可播放串流**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 在類 `MediaPlayer` 中

* **TVSDK支援CMAF和純串流播放，以播放加密的Widevine CTR。**

* **現在支援播放4K HEVC串流。**

* **並行廣告呼叫請求** - TVSDK現在可並行預取20個廣告呼叫請求。

**3.0版**

* **TVSDK 3.0支援高效率視訊編碼(HEVC)串流。**

* **即時——解析更靠近廣告標籤的廣告懶**
惰廣告解析現在可獨立解決每個廣告分隔。以前，廣告解決方案是分兩階段進行的：在播放開始之前已解決預卷問題，在播放開始之後，所有中／後滾動插槽都已合併。 透過這項增強功能，現在每個廣告插播都會在廣告提示點之前的特定時間解決。

>[!NOTE]
>
>「懶惰廣告解決」現在已變更為預設關閉，而且必須明確啟用。

新增API至`AdvertisingMetadata::setDelayAdLoadingTolerance`以取得與此廣告中繼資料相關的延遲廣告載入容限。\
現在，搜尋在準備後立即允許，搜尋廣告中斷將在搜尋完成前立即解決。\
支援信令模式`SERVER_MAP`和`MANIFEST_CUES`。

如需詳細資訊，請參閱[TVSDK 3.0 for Android Programmer&#39;s Guide](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md)中有關API和事件變更的說明。

* **更新 `targetSdkVersion` 至最新版**

已將`targetSdkVersion`從19更新為27，以順利運作。

* **Placement.Type getPlacementType()現在是介面TimelineMarker上的方法**

   此方法將返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置類型。 如果廣告中斷未解析，TimelineMarker介面上的getDuration()方法將傳回0。

**2.5.6版。**

* **TVSDK 2.5支援Android P。**

* **啟用背景音訊**

   若要在應用程式從前景移至背景時啟用音訊播放，當播放器處於「已準備」狀態時，應用程式應以true為引數呼叫`enableAudioPlaybackInBackground` MediaPlayer的API。

* **alwaysUseAudioOutputLatency(boolean val) in MediaPlayer類別**

設定後，在音訊時間戳記計算中使用輸出延遲。
布林參數val - True會在音訊時間戳記計算中使用音訊輸出延遲。

* **最佳化，即使頻寬速度突然下降，也能獲得最佳的播放體驗**

TVSDK現在會視需要取消持續區段的下載，並動態切換至適當的轉譯。 這是透過在位元速率之間無中斷地順暢切換而完成的。

**2.5.5版**

* **部分插入廣告分段**

   在加入廣告中間而不觸發部分受觀看廣告的追蹤的電視類體驗。\
   範例：使用者在90秒廣告插播（包含3個30秒廣告）的中間（40秒）加入。 這是分段內第二個廣告的10秒。

   * 第二個廣告會在剩餘期間（20秒）播放，接著是第三個廣告。

   * 不會引發已播放之部分廣告（第二個廣告）的廣告追蹤器。 只有第三個廣告的追蹤器會被觸發。

* **透過HTTPS安全載入廣告**

   Adobe Primetime提供選項，可要求在https上首次呼叫黃金時段廣告伺服器和CRS。

* **新增至CRS請求的AdSystem和Creative Id**

   現在在1401和1403要求中包含`AdSystem`和`CreativeId`作為新參數。

* **NetworkConfiguration類別中的API setEncodeUrlForTracking會** 移除URL中不安全的字元，因此應進行編碼。

**2.5.4版**

Android TVSDK v2.5.4提供下列更新和API變更：

* `WebViewDebbuging`預設值的變更

   `WebViewDebbuging` 值預設 `Fals`為e。若要啟用它，請在應用程式中呼叫`setWebContentsDebuggingEnabled(true)`。

* **OpenSSL和Curl版本升級**

   將libcurl更新為v7.57.0，將OpenSSL更新為v1.0.2k。

* VAST回應物件的應用程式層級存取

   引入新的API `NetworkAdInfo::getVastXml()`，可讓您存取應用程式的WAST回應物件。

**2.5.3版**

Android TVSDK v2.5.3提供下列更新和API變更。

* 建議所有使用CRS的TVSDK客戶使用TVSDK 2.5.3.85或最新版Android應用程式升級。 這將取代現有應用程式實作的下拉式。 在TVSDK升級後，在Proxy工具中檢查CRS創意URL要求(例如：Charles)，並確認路徑中的主機名稱和版本反映如下範例URL結構中。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的使用者代理可自訂：我們新增了一些新API來自訂使用者代理。

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* 在Android應用程式與TVSDK之間共用Cookie:Android TVSDK現在支援在JAVA層（儲存於Android應用程式的CookieStore）和C++ TVSDK層之間存取Cookie。 現在，您可以在原生C++圖層中設定和／或修改Cookie，因為Cookie會暴露在Java Cookie商店中。

* API變更：

   * 新增事件`CookiesUpdatedEvent`。 當Cookie更新時，媒體播放器會傳送它。

   * 新增API至`NetworkConfiguration::set/ getCustomUserAgent()`，以使用自訂使用者代理。

   * 新增API至`NetworkConfiguration::set/ getEncodedUrlForTracking`，以強制對不安全字元進行編碼。

   * 將新的API添加到`NetworkConfiguration::getNetworkDownVerificationUrl()`中，以在發生故障切換時設定網路驗證URL。

   * `TextFormat::treatSpaceAsAlphaNum`會新增新屬性，定義在顯示標題時是否將空間視為字母數字。

* `SizeAvailableEvent`中的更改。 以前，`getHeight()`和`getWidth()`方法（2.5.2中的`SizeAvailableEvent`）用於傳回由媒體格式傳回的「影格高度」和「影格寬度」。 現在它分別返回解碼器返回的輸出高度和輸出寬度。

* 緩衝行為的變更：緩衝行為已變更。 在緩衝區為空時，應用程式開發人員需自行決定要做什麼。 2.5.3在緩衝區空的情況下使用播放緩衝區大小。

**2.5.2版**

Android TVSDK v2.5.2提供重要的錯誤修正和一些API變更。

**2.5.1版**

Android 2.5.1中發行的重要新功能。

* **效能改進-** 全新的TVSDK 2.5.1架構提供多項效能改進。根據來自第三方基準研究的統計資料，新體系結構可將啟動時間縮短5倍，並減少掉幀數，與行業平均水準相比減少3.8倍：

* **VOD和即時的即時啟動——啟** 用即時啟動時，TVSDK會在播放開始前初始化媒體並緩衝媒體。由於您可以在背景同時啟動多個MediaPlayerItemLoader例項，因此可以緩衝多個串流。 當使用者變更頻道，而串流已正確緩衝時，新頻道上的播放會立即開始。 TVSDK 2.5.1也支援&#x200B;**live**&#x200B;串流的立即啟動。 即時視窗移動時，即時串流會重新緩衝。

* **改進的ABR邏** 輯——新的ABR邏輯以緩衝區長度、緩衝區長度變化率和測量頻寬為基礎。這確保了ABR在頻寬波動時選擇正確的比特率，並且還通過監視緩衝器長度變化的速率來優化比特率切換的實際發生的次數。

* **部分區段下載／子區段-** TVSDK會進一步縮小每個片段的大小，以便盡快開始播放。ts片段必須每隔兩秒有一個關鍵影格。

* **延遲廣告解析度-** TVSDK不會等到非預先播放廣告的解析度後，再開始播放，因此會縮短啟動時間。在所有廣告都解決之前，仍不允許搜尋和特技播放等API。 這適用於CSAI使用的VOD串流。 在廣告解析完成前，不允許搜尋和快進等操作。 對於即時串流，無法在即時事件期間啟用此功能以取得廣告解析度。

* **永久網路連線-** 此功能可讓TVSDK建立並儲存永久網路連線的內部清單。這些連線會重複用於多個請求，而不是為每個網路請求開啟新連線，然後在其後銷毀。 如此可提高網路程式碼的效率並減少延遲，進而提高播放效能。
當TVSDK開啟連線時，會要求伺服器進行*keep-alive*&#x200B;連線。 有些伺服器可能不支援此類連線，在這種情況下，TVSDK會回到每次要求的連線上。 此外，雖然永久連線預設會開啟，但TVSDK現在有設定選項，讓應用程式可視需要關閉永久連線。

* **並行下載-** 並行下載視訊和音訊，而非串列下載，可減少啟動延遲。此功能可讓HLS Live和VOD檔案播放，最佳化伺服器的可用頻寬使用，降低在執行中進入緩衝區的可能性，並將下載和播放之間的延遲降到最低。

* **平行廣告下載-** TVSDK會在點擊廣告插播前，平行預取與內容播放平行的廣告，因此可順暢地播放廣告和內容。

* **播放**

* **MP4內容播放-** MP4短片不需重新轉碼，就可在TVSDK中播放。

   >[!NOTE]
   >
   >MP4播放不支援ABR切換、特技播放、廣告插入、延遲音訊系結和子分段。

* **使用可調式位元速率(ABR)進行特技播放——此** 功能可讓TVSDK在特技播放模式下在iFrame串流之間切換。您可以使用非iFrame描述檔，以較低的速度進行特技播放。

* **更順暢的特技播放-** 這些增強功能可增強使用者體驗：

   * 在特技播放期間，根據頻寬和緩衝區描述檔選擇自適應比特率和幀速率

   * 使用主串流（而非IDR串流），以快速播放高達30 fps。

* **內容保護**

   * **基於解析度的輸出保護——此** 功能將播放限制與特定解析度關聯，提供更精細的DRM控制。

* **工作流程支援**

   * **直接計費整合-** 這會傳送帳單量度至Adobe Analytics後端，Adobe Primetime會針對客戶使用的串流進行認證。

   TVSDK會自動收集量度，並遵守客戶銷售合約，以產生計費所需的定期使用報告。 在每個串流開始事件上，TVSDK使用Adobe Analytics資料插入API，將計費量度(例如內容類型、啟用廣告插入的標幟，以及啟用DRM的標幟（根據可計費串流的持續時間）傳送至Adobe Analytics黃金時段擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 此帳單使用報表會按要求定期傳送給客戶。 這是計費功能的第一階段，僅支援使用計費。 您可使用說明檔案中所述的API，根據銷售合約來設定此API。 此功能預設為啟用。 若要關閉此功能，請參閱參考播放器範例。

   * **改進的容錯移轉支** 援——實作其他策略，以在主機伺服器、播放清單檔案和區段發生故障時，仍能持續不間斷播放。


* **廣告**

   * **Moat整合——支** 援Moat的廣告可檢視性度量。

   * **配套橫幅-** 配套橫幅會線上性廣告旁邊顯示，廣告結束後通常會繼續顯示在檢視中。這些橫幅可以是html（HTML程式碼片段）類型或是iframe（iframe頁面的URL）類型。

* **Analytics**

   * **VHL 2.0 —— 這是最** 新最佳化的視訊心率程式庫(VHL)整合，可自動收集Adobe Analytics的使用資料。API的複雜性已降低，以方便實施。 下載Android專用的VHL程式庫[v2.0.0，並解壓縮libs資料夾中的JAR檔案。](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)

* **SizeAvaliableEventListener**

   * `getHeight()` 以及 `getWidth()` 將分 `SizeAvailableEvent` 別以高度和寬度返回輸出的方法。顯示外觀比例的計算方式如下：

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      在Sar寬度和Sar高度方面，儲存高寬比也可用於計算幀寬和幀高：

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK現在支援存取儲存在Android應用程式CookieStore中的JAVA Cookie。 每當新Cookie作為&#x200B;**Set-Cookie**&#x200B;回應標題的一部分出現時，都會提供回呼API(onCookieUpdated)來記錄。 這些Cookie是以HttpCookie清單的形式提供，用於不同URI/網域，方法是使用CookieStore在該特定URI/網域上設定這些Cookie值。 同樣地，TVSDK中的Cookie值也會使用CookieStore新增API來更新。

## 功能矩陣{#feature-matrix}

適用於Android的TVSDK支援許多您可實作的功能，以新增功能至視訊應用程式。

在下列功能表格中，「Y」表示目前版本支援此功能。

| 功能 | 內容類型 | HLS |
|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD + Live | Y |
| FER —— 一般播放（播放、暫停、搜尋） | FER VOD | Y |
| 在廣告播放時尋找 | VOD + Live | 不支援 |
| HEVC Playback | VOD + Live | 僅限fMP4容器 |
| AC3和EAC3 | VOD + Live | 不支援 |
| MP3 | VOD | 不支援 |
| MP4內容播放 | VOD | Y |
| 自適應位速率切換邏輯 | VOD + Live | Y |
| 僅限音訊播放 | VOD + Live | Y |
| 多CDN支援 | VOD + Live | 不支援 |
| 使用純音訊媒體播放廣告 | VOD + Live | 不支援 |
| 隱藏字幕- 608/708 | VOD + Live | Y |
| 隱藏字幕- WebVTT | VOD + Live | Y |
| 資訊清單容錯移轉 | VOD + Live | Y |
| 高級故障切換 | VOD + Live | Y |
| QoS和播放器通知 | VOD + Live | Y |
| 支援Cookie標題 | VOD + Live | Y |
| 支援自訂HTTP標題 | VOD + Live | Y（允許列出） |
| 設定緩衝器控制參數 | VOD + Live | Y |
| 設定自適應位元速率控制 | VOD + Live | Y |
| 自訂資訊清單標籤 | VOD + Live | Y |
| 延遲音訊系結 | VOD + Live | Y |
| 302重新導向 | VOD + Live | Y |
| 使用偏移播放 | VOD + Live | Y |
| Trick Play | VOD + Live | Y |
| 特技遊戲中的慢動作 | VOD + Live | 不支援 |
| 流暢的特技播放（使用ABR） | VOD + Live | Y |
| ID3剖析 | VOD + Live | Y |
| 廣告封鎖 | VOD + Live | 不支援 |
| 立即啟動 | VOD + Live | 不支援 |
| 不連續標籤支援 | VOD + Live | Y |
| 302重新導向黏性 | VOD + Live | Y |

| 功能 | 內容類型 | HLS |
|---|---|---|
| 一般播放，啟用廣告 | VOD + Live | Y |
| 啟用廣告的FER內容 | VOD | Y |
| 預設廣告行為 | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4廣告 | VOD + Live | Y（來自CRS） |
| 啟用廣告的特技播放 | VOD + Live | Y |
| 僅限廣告 | VOD | Y |
| 定位參數 | VOD + Live | Y |
| 自訂參數 | VOD + Live | Y |
| 自訂廣告行為 | VOD + Live | Y |
| 自訂廣告標籤 | 即時 | Y |
| 自訂廣告解析器 | VOD + Live | Y |
| Freewheel自訂廣告解析程式 | VOD | Y |
| C3 | VOD + Live | 不支援 |
| 延遲廣告解決 | VOD | Y |
| 不連續標籤支援- SSAI | VOD + Live | Y |
| 配套廣告、橫幅廣告和可點選廣告 | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y(JS) |
| 提早退出廣告 | 即時 | Y |
| 以規則為基礎的創意優先順序 | VOD + Live | Y |
| CRS規則 | VOD + Live | Y |
| JSON廣告解析程式 | VOD + Live | 不支援 |
| Moat整合 | VOD + Live | Y |
| 部分插入廣告分段 | 即時 | Y |

| 功能 | 內容類型 | HLS |
|---|---|---|
| AES加密 | VOD + Live | Y |
| 範例AES加密 | VOD + Live | Y |
| Token化串流 | VOD + Live | Y |
| Widevine DRM | VOD + Live | 僅限fMP4容器 |
| Primetime DRM | VOD + Live | Y |
| 外部播放(RBOP) | VOD + Live | 僅限Primetime DRM |
| 授權輪換 | VOD + Live | 僅限Primetime DRM |
| 鍵旋轉 | VOD + Live | 僅限Primetime DRM |

| 功能 | 內容類型 | HLS |
|---|---|---|
| Adobe AnalyticsVHL整合 | VOD + Live | Y |
| 帳單 | VOD + Live | Y |

## 已解決問題{#resolved-issues}

如果解析度與報告的問題相關聯，則會顯示Zendesk參考，例如ZD#xxxxx。

**Android TVSDK 3.12**

本節提供TVSDK 3.12 Android版本中已解決問題的摘要。

* ZD#40584 - Primetime參考應用程式不會建立最新的Gradle版本。

### 已解決舊版中的問題

**Android TVSDK 3.11**

* ZD#41252 - WebVTT中的韓文字元在Android 7.1之後中斷。

**Android TVSDK 3.10**

* ZD#40340 —— 在列出所有TS(TypeScript)檔案的區塊後，嘗試播放時，應用程式會當機，出現「App Not Responding」錯誤。

**Android TVSDK 3.8**

* 未新增任何新問題。

**Android TVSDK 3.7**

* 未新增任何新問題。

**Android TVSDK 3.6**

* 未新增任何新問題。

**第3.5版**

* ZD#37503 —— 快取CRS規則的JSON回應，以避免重複要求。

**第3.4版**

* ZD#37996 —— 修正線性和VOD CMAF HEVC串流的播放不順暢問題。
* ZD#37706 —— 已修正字幕亂碼的問題。
* ZD#37622 —— 修正特定廣告的致命URISyntaxErrors問題。
* ZD#36938 —— 修正位元速率切換至中間位元速率，然後在結束特技播放後接上最高位元速率的問題。

**第3.3版**

* ZD#37394 - CMAF資產快速前進會在速度變更後造成不自然。
   * 修正特技播放期間，設定檔變更所發生的問題。
* ZD#37396 —— 某些中型和後型廣告追蹤事件遺失。
   * 修正廣告追蹤事件的特定案例。
* ZD#37491 - HTTP狀態碼中沒有錯誤meta。
   * 已處理在堆棧中傳播網路錯誤的問題。
* ZD#37808 —— 允許清單新的自訂標題。
   * 已新增SSAI_TAG支援，做為此修正的一部分。
* ZD#37622 —— 來自特定廣告Pod的URISyntax錯誤。
   * 修正當客戶Android應用程式提供包含未編碼%的廣告時，串流播放當機的問題
* ZD#37631 —— 適用於Android TVSDK的主資訊清單重試機制。
   * 在網路組態中新增API以處理此增強功能。 如果未使用此API，則不會重試資訊清單。 如果已使用清單，則會重試清單以處理網路錯誤和逾時。

**第3.2版**

* ZD#37493-即時播放的追蹤信標不會間歇性地針對順序中的第一個廣告引發。
* ZD#36985- VMAP回應中不會針對空的廣告插播傳送追蹤信標。
* ZD#37134 - TVSDK間歇性地擲出錯誤的ID以回應VMAP。

**3.0版**

* ZD#33740 - TVSDK在建立MediaPlayer物件並呼叫replaceCurrentResource()後，就會擲出不需要的警告

   * 已改善先前的修正，只在播放器處於暫停狀態時呼叫restore

* ZD#36442 —— 每個新播放都會中斷遠端除錯工作階段，因此無法除錯。

   * Web檢視預設無法進行除錯，因為預設未啟用除錯。 應用程式應視需要啟用除錯，方法是在從MediaPlayer.getCustomAdView()傳回的物件上呼叫setWebContentsDebuggingEnabled(true)。

* ZD#33688 —— 支援及時解決方案

   * 廣告分段會在廣告分段位置之前的指定間隔內解決。

* ZD#36441 —— 即時視窗持續時間持續增加超過5分鐘，造成多個問題。

   * 修正在計算虛擬即時點時，會新增兩次virtualStartTime的問題，造成此問題。

**Android TVSDK 2.5.6**

* ZD #34992 —— 隱藏字幕中的語言是空的。

   * 修正TVSDK未從主資訊清單剖析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS以取得標題追蹤詳細資訊的案例。

* ZD #35078 - Android P驗證。

   * TVSDK 2.5.6已通過最新Android P測試版本的驗證。 由於新的Android作業系統，未發現任何問題。

* ZD #34149 —— 播放器即使遇到錯誤，仍會繼續要求艙單。

   * 修正即使所有描述檔都關閉，TVSDK仍會重複呼叫的情況（404錯誤）。

* ZD #31533 —— 在應用程式傳送至背景後，在Android上播放音訊。

   * 已新增應以&#39;True&#39;作為引數（當播放器處於「已準備」狀態時）呼叫的MediaPlayer的`enableAudioPlaybackInBackground` API，以啟用應用程式在背景時的音訊播放。

**Android TVSDK 2.5.5**

* ZD #21647 —— 當實際視訊大小為640x360時，Android TVSDK會通知640x368。

   * 由於可變m_nOutputHeight（在AndroidMCVideoDecoder內）會以影格高度而非實際輸出高度更新。 在getVideoFrame函式中進行相關變更，以正確計算m_nOutputHeight。

* ZD #26614 —— 緊急——第三方廣告服務／程式化——未能提供印象。

   * 在XML剖析中處理「空格」在「等號」（例如&lt;VAST version =&quot;2.0&quot;>）之前時，問題可重複的案例，以增強先前的修正

* ZD #29296 - Android:將AdSystem和Creative ID新增至CRS請求。

   * 現在在1401和1403個請求中加入「AdSystem」和「CreativeId」作為新參數。

* ZD #33062 - TVSDK在CDATA節點下的VAST響應中發生管道字元時崩潰

   * NetworkConfiguration類別中的API setEncodeUrlForTracking會移除為URL中不安全的字元以進行編碼

* ZD #33063 - CRS檔案選擇邏輯中斷- TVSDK並未傳送CRS的webm格式要求，而是傳送3gpp檔案。

   * 已修正邏輯。 在使用具有webm和3gpp格式的媒體檔案時，CRS請求將發送給webm。 當使用具有3gpp格式的媒體檔案時，CRS要求會針對最高位元速率的3gpp檔案傳送。

* ZD #33125 - Android應用程式在VMAP中當機時會有特定的DoubleClick標籤。

   * 已修正藍本，以避免當機。

* ZD #32256 —— 許可輪換和密鑰輪換問題-Adobe訪問

   * 已修正使用SampleAES內容的DRM中繼資料來初始化區段的問題。 適用於AES128內容。

* ZD #33619 —— 快速轉送正在成長的播放清單內容，其停留在即時點附近的緩衝狀態。

   * 以特技播放模式跨越即時點時處理案例

* ZD #34151 - TimedMetadata物件順序錯誤。

   * 如果兩個TimedMetadata事件屬於時間軸中的同一時間，它們會以隨機順序顯示。 維持原始訂單。

* ZD #34189 —— 尋求開始廣告插播時的問題。

   * 問題是SSAI廣告使用不連續性縫合。 原因是當我們開始尋找這類廣告時，我們會尋找一個關鍵畫格，卻找不到它。 原因是廣告的最小音訊時間戳記早於最小視訊時間戳記。 因此，我們最終在錯誤的fragmentDump資料處搜索關鍵幀。 已修正。

* ZD #34528 —— 在FireTV第3代轉換器上，視頻解析度未升級到640x360以上。

   * 已增強修正功能，加入最新的韌體更新

* ZD #34793 - TVSDK 2.5.x，用於在VideoEngine假設auditudeSettings可用而未提供時，與自訂內容解析器一起當機。

   * 當機是由於Null共用指針(auditudeSettings)上的函式呼叫所致。 在VideoEngineTimeline::placeToSourceTimeline()中新增條件檢查，以在呼叫該物件上的任何項目之前，先確定auditudeSettings是可用的。

* ZD #32584 —— 無法訪問WAST響應的&lt;Extensions>節點中顯示的完整資訊。

   * 修正XML剖析的問題，現在NetworkAdInfo提供&lt;Extensions>節點中顯示的完整資訊

* ZD #35086 —— 在特定VMAP回應的情況下，無法從播放器取得完整的擴充功能資料。

   * 問題是特定於擴充XML，因為如果擴充XML在屬性值中有雙引號，XML剖析就無法運作。 已修正問題。

**Android TVSDK 2.5.4**

* ZenDesk#33659 —— 播放工作階段，可啟用Webview遠端除錯。

WebViewDebbuging預設為False。 若要啟用除錯，請使用setWebContentsDebuggingEnabled(true)，透過應用程式設為true。

* ZenDesk#33011 —— 如果CRS請求失敗，廣告時間軸無法解決。

   當對廣告的CRS請求失敗時，時間軸會解決，而剩餘的廣告則會播放。

* ZenDesk#34528 - FireTV第三代轉換器的視訊解析度無法升級至640x360以上。

   視訊解析度會切換為位元速率切換。

* ZenDesk#33192 —— 當透過AudioUpdatedEventListener::onAudioUpdated擷取音軌時，音訊軌的名稱為null。

   在FireTV Stick的幾種情況下，當沒有實際的音訊更新時，onAudioUpdate事件會被觸發。 現在已修正。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自訂標籤訂閱無法運作。

   我們會將ID3資料以位元組陣列（以支援APIC或一般資料）傳回給用戶端，而1.4傳回字串中則是如此。 位元組陣列不處理以空值結尾的字元本身，因此，它對客戶端顯示特殊字元。 此問題已修正。
* Zendesk#32670 —— 播放器未故障切換至冗餘播放清單

   現在運作正常，且setNetworkDownVerificationUrl如預期般運作。
* Zendesk#32369 —— 隱藏字幕顯示不同的顏色垃圾訊息或偽影。

   CC故障問題已修正至最新版本
* Zendesk#25590 —— 增強：TVSDK Cookie儲存（C++至JAVA）

   Android TVSDK現在支援在JAVA層（儲存於Android應用程式的CookieStore）和C++ TVSDK層之間存取Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎沒有PTPLAY-20269的修正

   此問題已修正並整合至2.5.2分支。
* Zendesk#31806 - Auditude在準備工作中堅持

   Player因回應xml有空標籤而停留在「準備」狀態。 現在問題已修正。
* Zendesk#31727 - TVSDK 2.5隱藏字幕字元會遺失或拼錯。

   問題已修正，我們不會刪除／拼字錯誤。
* Zendesk#31485 - 2.5版DrmManager

   通過新的DrmManager（上下文內容）建立DrmManager時存在一些問題。 實施DRMService類，該類將提供DRMManager。
* Zendesk#32794- 1080P解析度串流未在Android上播放

   我們在2.5中變更了SizeAvailableEvent和Previouly、getHeight()和getWidth()方法，用以傳回媒體格式傳回的「影格高度」和「影格寬度」。 現在，它分別返回解碼器返回的輸出高度和輸出寬度。
* Zendesk #19359Flash Player因在設定層級資訊清單中的#EXT-X-FAXS-CM屬性位置而當機。

   #EXT-X-FAXS-CM標籤必須一律出現在頂端播放清單中，個別位元速率或區段才會出現在播放清單中。

**Android TVSDK 2.5.2**

* Zendesk#17305非不透明背景的隱藏字幕中的偽物。

   setTreatSpaceAsAlphaNum屬性會公開在TextFormat中。 依預設，屬性為False。 在用戶端中將屬性設為True，以解決隱藏空間問題。

* Zendesk#25097 CC顯示器具有具有CC設定的視覺偽像。

   setTreatSpaceAsAlphaNum屬性會公開在TextFormat中。 依預設，屬性為False。 在用戶端中將屬性設為True，以解決隱藏空間問題。

* Zendesk #31620從TVSDK播放器傳出的使用者代理字串被截斷。

   使用者代理字串在128個字元後不會再遭截斷。

   Adobe Primetime版本字串會新增至系統使用者代理。

* Zendesk #30809遺失SEEK_END事件可防止應用程式轉換至播放狀態。
* Zendesk #30415隱藏字幕的「青色」色現在較舊的Primetime TVSDK版本更深藍色（綠松石）。

   顏色從「深藍色」(DarkCyan)變更為「青色」(Cyan)。

* Zendesk #30727 VOD廣告無法下載／解決。

   在VMAP XML中，如果有空的VAST標籤，而沒有明確的結束標籤(『&lt;/VAST>&#39;)，且後面沒有新行字元，則VMAP XML無法正確解析，廣告可能無法播放。

**Android TVSDK 2.5.1**

* 特定裝置(Samsung Galaxy Tab 4)當機；VOD DRM LBA含Auditude，然後按一下廣告。
* VHL —— 從偏移開始內容時會傳送錯誤的心率呼叫。
* 播放VPAID廣告時，VHL心率eartbeat會呼叫event:type:play廣告，但會遺失。
* 進入「完成」狀態後，播放器會回到SKIP adBreakPolicy的播放狀態，以處理後段廣告。
* Cookie未附加至傳出廣告回呼。
* 廣告提示點不可見。
* HLS將不會載入具有獨立EAC3 SAP跟蹤的EAC3。
* 當TVSDK在Media Player還原後收到「畫面開啟」意圖時，播放器會當機。

## 已知問題和限制{#known-issues-and-limitations}

**Android TVSDK 3.11**

* 未新增任何限制。

### 舊版的已知問題和限制

**Android TVSDK 3.10**

* 未新增任何限制。

**Android TVSDK 3.8**

* 未新增任何限制。

**Android TVSDK 3.7**

* 未新增任何限制。

**Android TVSDK 3.6**

* 未新增任何限制。

**Android TVSDK 3.5**

* 沒有新的限制。

**Android TVSDK 3.4**

* ID3、隱藏字幕、延遲系結音訊支援尚未針對CMAF(CBC)串流進行驗證。
* 在CMAF流的特技播放中，由於視頻失真會在頂部出現，所以在某些裝置上存在重現性差的問題。

**Android TVSDK 3.3**

* clcp:c608標題不支援CMAF串流播放。

**Android TVSDK 3.2**

* TVSDK 3.2不支援CMAF Sample AES和AES128串流播放。
* HEVC CMAF串流不包含隱藏字幕播放的支援。
* 當圍繞非加密段執行搜索時，WV加密流會出現綠色。
* CMAF串流不支援ID3事件。
* HLS串流不支援TTML標題格式。

**Android TVSDK 3.0**

* HEVC支援在此版本中有下列限制

   * 不支援DRM
   * CC(CEA 608/708)支援未驗證
   * 4K支援尚未提供
   * 未驗證ID3標籤支援

* 對於廣告進度事件，時間軸列可能無法反映100%精確的廣告播放時間。 因應措施是，您可使用`adcompleteevent`來瞭解廣告播放完成並更新UI，以用於更新時間軸列、移除廣告相關UI等各種用途。
* 從VMAP傳回的龐大廣告呼叫不符合「及時前瞻」位置。

**Android TVSDK 2.5.6**

* 不支援同時進行多個VMAP廣告插播。

**Android TVSDK 2.5.3**

此版本有下列問題：

* 即時視訊播放在低端裝置上可能發生音訊——視訊同步問題，或網路狀況不佳。
* 對於FER串流，virtualTime和localTime可能不同。 同時，具有偏移的FER也無效。
* 當搜尋「延遲系結音訊」內容時，播放可能會卡住。
* WebVTT標題可能會間歇性地對即時內容不同步。
* 在廣告中斷後，偶爾可看到快速播放幾個影格。
* 有時，即使已播放廣告，「三重包裝函式廣告分段」仍會擲回303錯誤。

**Android TVSDK 2.5.2**

此版本有下列問題：

* 在低端裝置上，即時視訊播放可能會發生音訊——視訊同步問題。
* 當嘗試到VOD媒體結尾時，播放可能會停止。
* 對於FER串流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。

**Android TVSDK 2.5.1**

此TVSDK版本有下列問題：

* 在低端裝置上，即時視訊播放可能會發生音訊——視訊同步問題。
* 對於FER串流，virtualTime和localTime可能不同。 此外，具有偏移的FER不起作用。
* 在VMAP XML中，如果有空的VAST標籤沒有明確的結束標籤(&lt;/VAST>)，而後面沒有新行，則VMAP XML無法正確解析，廣告可能無法播放。
* 不支援VPAID後置記錄。

## 實用資源{#helpful-resources}

* [系統需求](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [TVSDK 3.10 for Android程式設計人員指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API Document](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html)  —— 每個Java類都有對應的C++類，而C++檔案包含比Javadoc更多的說明性資料，請參閱C++檔案以進一步瞭解Java API。
* [Android專用TVSDK 1.4至2.5(Java)移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 如需處理畫面開啟／關閉藍本的資訊，請參閱建置中包含的`Application_Changes_for_Screen_On_Off.pdf`檔案。
* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。
