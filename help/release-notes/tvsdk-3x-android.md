---
title: Android適用的TVSDK 3.14發行說明
description: Android適用的TVSDK 3.14發行說明說明TVSDK Android 3.14中的新增或變更、已解決和已知問題及裝置問題
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 988bcf8cbc0175e15bcc899a6f6954cc31c5e127
workflow-type: tm+mt
source-wordcount: '5480'
ht-degree: 0%

---

# Android適用的TVSDK 3.14發行說明 {#tvsdk-for-android-release-notes}

Android適用的TVSDK 3.14發行說明說明TVSDK Android 3.14中的新增或變更、已解決和已知問題以及裝置問題。

發佈的samples/目錄中，Android參考播放器隨Android TVSDK一併包含。 隨附的README.md檔案說明如何建立參考播放器。

>[!NOTE]
>
>若要如隨此版本分發的README.md所述成功建立參考播放器，請務必執行下列操作：
>
>1. 從[https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)下載VideoHeartbeat.jar（Android適用的VideoHeartbeat程式庫v2.0.0）
>1. 將VideoHeartbeat.jar解壓縮至libs/資料夾。


Android適用的TVSDK提供比舊版更多的效能改善。 除了Multi-CDN支援外，提供高品質的檢視體驗，並包含1.4版的所有功能。

發行說明的[功能矩陣](#feature-matrix)區段中提供支援和不支援的完整功能集。

## Android TVSDK 3.14

此版本修正了當VAST回應中的[!UICONTROL ClickTracking]、[!UICONTROL CustomClick]或[!UICONTROL CompanionClickTracking]元素的[!UICONTROL CDATA]節點為空時，應用程式當機的問題。

### 舊版中的新功能和增強功能

**Android TVSDK 3.13**

Widevine DRM流凍結或顯示FireTV設備上的ABR開關上的黑幀，這些設備包括Fire TV第3代Linte和Fire TV Cube第1和第2代設備。

若要解決此問題，請在開始播放之前，為指定的Fire TV裝置設定API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)`。 預設值為false。

**Android TVSDK 3.12**

Primetime參考應用程式的Gradle版本已更新至5.6.4版。

若要使用Android Studio來設定及執行參考應用程式，請依照`TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`上TVSDK zip所提供之ReadMe檔案的指示操作。

在[已解決的問題](#resolved-issues)區段中會提及目前版本中修正的主要客戶問題。

**Android TVSDK 3.11**

* **允許擷取保護系統特定標題(PSSH)方塊**  - TVSDK允許擷取與目前載入的媒體資源相關聯的保護系統特定標題方塊。新增API `getPSSH()`至`com.adobe.mediacore.drm.DRMManager`。

如需詳細資訊，請參閱[Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md)。

**Android TVSDK 3.10**

此版本著重於修正[已解決的問題](#resolved-issues)區段中提及的常見客戶問題。

**Android TVSDK 3.9**

* **透過HTTPS進行安全傳送**  - Android TVSDK 3.9推出透過HTTPS的安全傳送功能，以無可比擬的規模和效能安全地傳送內容。

   為了透過HTTPS啟用安全傳送，`NetworkConfiguration`類別中推出了新API。

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **具有部分廣告插播功能的前段支援**  — 透過此增強功能，TVSDK 3.8支援具有部分廣告插播功能(PABI)的前段廣告。

前段廣告（如果可用）會播放，然後內容會從直播點模擬直播電視的體驗來播放。

**Android TVSDK 3.7**

* 對於Widevine測試內容，DRManager類中的新API `setMediaDrmCallback`將公開以覆蓋MediaDrmCallback介面的預設實現。

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* 修正未在C++層（Android 64位元）中處理`MediaPlayerEvent.ITEM_UPDATED`的AppCrash錯誤。

**Android TVSDK 3.6**

* **增強您的應用程式以符合64位元需求**  — 原生程式 `(libAVEAndroid.so)` 庫現已升級，並可在兩個版本中使用。現有armeabi（32位）本機程式庫位置已從`/framework/Player to /framework/Player/armeabi`變更，並在`/framework/Player/arm64-v8a.`中引入額外的arm64-v8a（64位）程式庫

**版本3.5**

* **準時廣告解決**  - TVSDK 3.5會從時間軸移除對已播放廣告的支援。

* **啟用離線播放支援**  — 透過離線播放，使用者現在可以下載視訊內容至其裝置，並在未連線時觀看。如需詳細資訊，請參閱「[使用Android的離線播放](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)」。

**版本3.4**

* TVSDK現在支援CMAF資料流播放，以播放CBC加密和純資料流。

**版本3.3**

* **API變更**

   * `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*`新增了新的API，以處理網路錯誤和逾時。
      * 其中(n)為重試次數。

**版本3.2**

* **平行廣告解析度和資訊清單下載支援**

   * TVSDK 3.2支援同時解析度，而非VMAP以外所有廣告請求和廣告插播的循序解析度。

   * 同時下載廣告插播中的所有廣告資訊清單。

* **啟用廣告解析度和資訊清單下載逾時支援。**

   * 使用者現在可以設定整體廣告解析度和資訊清單下載的逾時值。  若是VMAP，逾時值會套用至個別廣告插播，因為所有廣告插播都會依序解析。

* **在AdvertisingMetadata類別中推出新API:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **從AdvertisingMetadata類別中移除以下API:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **使用AC3/EAC3音頻編解碼器啟用流的回放**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` 在類 `MediaPlayer` 中

* **TVSDK支援CMAF和純資料流播放，以供加密的Widevine CTR播放。**

* **現在支援播放4K HEVC資料流。**

* **平行廣告呼叫請求**  - TVSDK現在會同時預取20個廣告呼叫請求。

**版本3.0**

* **TVSDK 3.0支援高效視訊編碼(HEVC)串流。**

* **「準時」 — 解析靠近廣告標籤的廣**
告「延遲廣告解決」現在可獨立解析每個廣告插播。之前，廣告解決是分兩階段的方法：已在播放開始前解決前段，且在播放開始後結合所有中段/後段槽。 透過這項增強功能，每個廣告插播現在都會在廣告提示點之前的特定時間解決。

>[!NOTE]
>
>「延遲廣告解決」現在已變更為預設關閉，且需明確啟用。

新增API至`AdvertisingMetadata::setDelayAdLoadingTolerance`，以取得與此廣告中繼資料相關聯的延遲廣告載入容差。\
現在，搜尋可在PREPARATION後立即允許，搜尋廣告插播將會在搜尋完成前立即解決。\
支援信令模式`SERVER_MAP`和`MANIFEST_CUES`。

如需詳細資訊，請參閱[TVSDK 3.0 for Android程式設計師指南](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) ，了解API和事件變更的相關資訊。

* **更 `targetSdkVersion` 新至最新版本**

將`targetSdkVersion`從19更新至27，以順利運作。

* **Placement.Type getPlacementType()現在是介面TimelineMarker上的方法**

   此方法將返回Placement.Type.PRE_ROLL、Placement.Type.MID_ROLL或Placement.Type.POST_ROLL的放置類型。 如果廣告插播未解析，TimelineMarker介面上的getDuration()方法將返回0。

**版本2.5.6。**

* **TVSDK 2.5支援Android P。**

* **啟用背景音訊**

   若要在應用程式從前景移至背景時啟用音訊播放，當播放器處於「已準備」狀態時，應用程式應以true作為引數，呼叫`enableAudioPlaybackInBackground` MediaPlayer的API。

* **MediaPlayer類別中的alwaysUseAudioOutputLatency(boolean val)**

設定後，在音訊時間戳記計算中使用輸出延遲。
布林參數val - True將在音訊時間戳計算中使用音訊輸出延遲。

* **最佳化，即使頻寬速度突然下降，仍可獲得最佳播放體驗**

TVSDK現在會視需要取消持續區段的下載，並動態切換至適當的轉譯。 這是透過在位元速率之間無縫切換而完成，而不會中斷。

**版本2.5.5**

* **部分廣告插播插入**

   加入廣告中間而不引發部分已觀看廣告追蹤的類似電視體驗。\
   範例：使用者在由三個30秒廣告組成的90秒廣告插播的中間（40秒）加入。 這是插播中第二個廣告的10秒。

   * 第二個廣告會在剩餘期間（20秒）播放，接著第三個廣告。

   * 未引發部分廣告播放（第二個廣告）的廣告追蹤器。 只觸發第三個廣告的追蹤器。

* **透過HTTPS安全載入廣告**

   Adobe Primetime提供可要求首次呼叫primetime廣告伺服器和CRS over https的選項。

* **新增至CRS請求的AdSystem和創作ID**

   現在將`AdSystem`和`CreativeId`納入為1401和1403請求中的新參數。

* **NetworkConfiguration類中的API setEncodeUrlForTracking** 會移除URL中不安全的字元，因此應進行編碼。

**版本2.5.4**

Android TVSDK v2.5.4提供下列更新和API變更：

* `WebViewDebbuging`預設值的變更

   `WebViewDebbuging` 值預設為 `Fals`e。若要啟用，請呼叫應用程式中的`setWebContentsDebuggingEnabled(true)`。

* **OpenSSL和Curl版本升級**

   將libcurl更新為v7.57.0，並將OpenSSL更新為v1.0.2k。

* VAST回應物件的應用程式層級存取

   導入了新的API `NetworkAdInfo::getVastXml()` ，提供對應用程式的VAST回應物件的存取。

**版本2.5.3**

Android TVSDK v2.5.3提供下列更新和API變更。

* 建議所有使用CRS的TVSDK客戶使用TVSDK 2.5.3.85或Android上的最新版本，將其應用程式升級。 這將取代現有應用程式實作的下拉式清單。 TVSDK升級後，在Proxy工具中檢查CRS創意URL要求(例如：Charles)，並確認路徑中的主機名稱和版本反映如下列範例URL結構中。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的使用者代理可自訂：我們已新增一些新API來自訂使用者代理。

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* 在Android應用程式和TVSDK之間共用Cookie:Android TVSDK現在支援在JAVA層（儲存於Android應用程式的CookieStore）和C++ TVSDK層之間存取Cookie。 現在，可以在原生C++層中設定和/或修改Cookie，因為Cookie會公開至Java Cookie Store。

* API變更：

   * 已新增新事件`CookiesUpdatedEvent`。 更新Cookie時，會由媒體播放器發送。

   * 新增API至`NetworkConfiguration::set/ getCustomUserAgent()`以使用自訂使用者代理。

   * `NetworkConfiguration::set/ getEncodedUrlForTracking`新增了新的API，以強制對不安全字元進行編碼。

   * 將新API添加到`NetworkConfiguration::getNetworkDownVerificationUrl()`，以在發生故障轉移時設定網路驗證URL。

   * `TextFormat::treatSpaceAsAlphaNum`新增了新屬性，定義在顯示字幕時是否將空間視為英數字元。

* `SizeAvailableEvent`中的更改。 以前，2.5.2中`getHeight()`和`getWidth()`方法用於傳回影格高度和影格寬度（由媒體格式傳回）。 `SizeAvailableEvent`現在，它分別傳回由解碼器傳回的輸出高度和輸出寬度。

* 緩衝行為中的變更：緩衝行為已變更。 在緩衝空白時，由應用程式開發人員決定要執行什麼動作。 2.5.3在緩衝區空時使用播放緩衝區大小。

**版本2.5.2**

Android TVSDK v2.5.2提供重要錯誤修正和一些API變更。

**版本2.5.1**

Android 2.5.1中發行的重要新功能。

* **效能改善 —** 全新TVSDK 2.5.1架構提供多項效能改善。根據來自第三方基準研究的統計資料，新體系結構提供的啟動時間比行業平均水準減少5倍，掉格減少3.8倍：

* **適用於VOD和即時的「即時開啟」 —** 當您啟用「即時開啟」時，TVSDK會在播放開始前初始化並緩衝媒體。因為您可以在背景中同時啟動多個MediaPlayerItemLoader例項，所以可以緩衝多個資料流。 當使用者變更頻道，且資料流已正確緩衝時，新頻道上的播放會立即開始。 TVSDK 2.5.1也支援&#x200B;**live**&#x200B;串流的「即時開啟」。 即時視窗移動時，即時資料流會重新緩衝。

* **改進的ABR邏輯 —** 新的ABR邏輯基於緩衝區長度、緩衝區長度變化率和測量頻寬。這確保ABR在頻寬波動時選擇正確的位速率，並通過監視緩衝長度變化的速率來優化位速率交換機實際發生的次數。

* **部分區段下載/子分段 —** TVSDK會進一步縮小每個片段的大小，以便盡快開始播放。ts片段必須每兩秒有一個關鍵幀。

* **延遲廣告解析度 —** TVSDK不會在開始播放之前等待非前段廣告的解析度，因而縮短了啟動時間。在所有廣告都解決之前，仍不允許使用搜尋和特技播放等API。 這適用於與CSAI搭配使用的VOD資料流。 在廣告解析完成前，不允許執行搜尋和快速前進等操作。 針對即時資料流，無法在即時事件期間為廣告解析啟用此功能。

* **永久性網路連線 —** 此功能可讓TVSDK建立並儲存持續性網路連線的內部清單。這些連接可重複用於多個請求，而不是為每個網路請求開啟新連接，然後在之後銷毀它。 這可提高網路程式碼的效率並減少延遲，進而提高播放效能。
TVSDK開啟連線時，會要求伺服器提供*keep-alive*&#x200B;連線。 某些伺服器可能不支援此類型的連線，在此情況下，TVSDK會回復為每個要求重新建立連線。 此外，雖然永久連線預設會開啟，但TVSDK現在提供設定選項，讓應用程式可視需要關閉永久連線。

* **並行下載 —** 並行下載視訊和音訊，而非串列下載，可減少啟動延遲。此功能可讓HLS Live和VOD檔案播放、從伺服器最佳化可用頻寬使用、降低在執行不充分的情況下進入緩衝區的可能性，以及將下載和播放之間的延遲降至最低。

* **平行廣告下載 —** 在點擊廣告插播前，TVSDK會預先擷取與內容播放平行的廣告，進而順暢播放廣告和內容。

* **播放**

* **MP4內容播放 —** MP4短片不需要重新轉碼以在TVSDK內播放。

   >[!NOTE]
   >
   >MP4播放不支援ABR切換、特技播放、廣告插入、延遲音訊系結和子分段。

* **使用適用性位元速率(ABR)進行特技播放 —** 此功能可讓TVSDK在特技播放模式下，在iFrame資料流之間切換。您可以使用非iFrame描述檔以較低的速度進行特技播放。

* **更流暢的特技播放 —** 這些改善功能可增強使用者體驗：

   * 基於頻寬和緩衝配置檔案的特技播放期間自適應比特率和幀速率選擇

   * 使用主資料流（而非IDR資料流）來取得高達30 fps的快速播放。

* **內容保護**

   * **基於解析度的輸出保護 —** 此功能將播放限制與特定解析度系結，提供更精細的DRM控制。

* **工作流程支援**

   * **直接計費整合 —** 這會將計費量度傳送至Adobe Analytics後端，經Adobe Primetime認證，可供客戶使用的資料流。

   TVSDK會依據客戶銷售合約自動收集量度，以產生計費所需的定期使用量報表。 在每個串流開始事件上，TVSDK會使用Adobe Analytics資料插入API，將計費量度（例如內容類型、啟用廣告插入的標幟，以及根據可計費串流的持續時間啟用drm的標幟）傳送至Adobe Analytics Primetime擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 此計費使用情況報告會按請求定期發送給客戶。 這是計費功能的第一階段，僅支援使用計費。 您可以使用檔案中所述的API，根據銷售合約進行設定。 此功能預設為啟用。 若要關閉此功能，請參閱參考播放器範例。

   * **改善故障轉移支援 —** 實作其他策略以繼續不間斷播放，儘管主機伺服器、播放清單檔案和區段失敗。


* **廣告**

   * **Moat整合 —** 支援從Moat進行廣告檢視度測量。

   * **伴隨橫幅 —** 伴隨橫幅會與線性廣告一併顯示，且通常會在廣告結束後繼續顯示在檢視上。這些橫幅可以是html類型(HTML片段)或是iframe類型（iframe頁面的URL）。

* **Analytics**

   * **VHL 2.0 -** 這是最新最佳化的視訊心率程式庫(VHL)整合，可自動收集Adobe Analytics的使用資料。API的複雜度已降低，以便輕鬆實作。 下載Android適用的VHL程式庫[v2.0.0，並在libs資料夾中解壓縮JAR檔案。](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases)

* **SizeAvaliableEventListener**

   * `getHeight()` 和方 `getWidth()` 法現 `SizeAvailableEvent` 在會分別以高度和寬度傳回輸出。顯示外觀比例的計算方式如下：

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      在Sar寬度和Sar高度方面，儲存長寬比也可用於計算幀寬和幀高：

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK現在支援存取儲存在Android應用程式CookieStore中的JAVA Cookie。 提供回呼API(onCookiesUpdated)，以在每次有新Cookie來自&#x200B;**Set-Cookie**&#x200B;回應標題時進行記錄。 使用CookieStore在該特定URI/網域上設定這些Cookie值，即可將這些Cookie作為用於不同URI/網域的HttpCookie清單使用。 同樣地，TVSDK中的Cookie值也會使用CookieStore新增API來更新。

## 特徵矩陣 {#feature-matrix}

Android適用的TVSDK支援許多您可實作的功能，以為視訊應用程式新增功能。

在以下的功能表中，「Y」表示當前版本支援該功能。

| 功能 | 內容類型 | HLS |
|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD +正式播放 | Y |
| FER — 一般播放（播放、暫停、搜尋） | 傳送VOD | Y |
| 在廣告播放時搜尋 | VOD +正式播放 | 不支援 |
| HEVC播放 | VOD +正式播放 | 僅限fMP4容器 |
| AC3和EAC3 | VOD +正式播放 | 不支援 |
| MP3 | VOD | 不支援 |
| MP4內容播放 | VOD | Y |
| 自適應位速率切換邏輯 | VOD +正式播放 | Y |
| 僅音頻播放 | VOD +正式播放 | Y |
| 多CDN支援 | VOD +正式播放 | 不支援 |
| 使用僅限音訊媒體播放廣告 | VOD +正式播放 | 不支援 |
| 隱藏式字幕 — 608/708 | VOD +正式播放 | Y |
| 隱藏式字幕 — WebVTT | VOD +正式播放 | Y |
| 清單故障切換 | VOD +正式播放 | Y |
| 高級故障切換 | VOD +正式播放 | Y |
| QoS和播放器通知 | VOD +正式播放 | Y |
| 支援Cookie標題 | VOD +正式播放 | Y |
| 支援自訂HTTP標題 | VOD +正式播放 | Y（允許列出） |
| 設定緩衝控制參數 | VOD +正式播放 | Y |
| 設定自適應位速率控制 | VOD +正式播放 | Y |
| 自訂資訊清單標籤 | VOD +正式播放 | Y |
| 延遲音頻綁定 | VOD +正式播放 | Y |
| 302重新導向 | VOD +正式播放 | Y |
| 具有偏移的播放 | VOD +正式播放 | Y |
| 戲法 | VOD +正式播放 | Y |
| 特技遊戲中的慢動作 | VOD +正式播放 | 不支援 |
| 流暢的特技播放（使用ABR） | VOD +正式播放 | Y |
| ID3解析 | VOD +正式播放 | Y |
| 廣告封鎖 | VOD +正式播放 | 不支援 |
| 立即啟用 | VOD +正式播放 | 不支援 |
| 不連續標籤支援 | VOD +正式播放 | Y |
| 302重新導向黏著度 | VOD +正式播放 | Y |

| 功能 | 內容類型 | HLS |
|---|---|---|
| 一般播放，啟用廣告 | VOD +正式播放 | Y |
| 啟用廣告的FER內容 | VOD | Y |
| 預設廣告行為 | VOD +正式播放 | Y |
| VAST 2.0/3.0 | VOD +正式播放 | Y |
| VMAP 1.0 | VOD +正式播放 | Y |
| MP4廣告 | VOD +正式播放 | Y（來自CRS） |
| 啟用廣告的特技播放 | VOD +正式播放 | Y |
| 僅廣告 | VOD | Y |
| 目標參數 | VOD +正式播放 | Y |
| 自訂參數 | VOD +正式播放 | Y |
| 自訂廣告行為 | VOD +正式播放 | Y |
| 自訂廣告標籤 | 即時 | Y |
| 自訂廣告解析器 | VOD +正式播放 | Y |
| 自由輪自訂廣告解析器 | VOD | Y |
| C3 | VOD +正式播放 | 不支援 |
| 延遲廣告解決 | VOD | Y |
| 不連續標籤支援 — SSAI | VOD +正式播放 | Y |
| 隨附廣告、橫幅廣告和可點按廣告 | VOD +正式播放 | Y |
| VPAID 2.0 | VOD +正式播放 | Y(JS) |
| 搶先退出廣告 | 即時 | Y |
| 以規則為基礎的創意內容優先順序 | VOD +正式播放 | Y |
| CRS規則 | VOD +正式播放 | Y |
| JSON廣告解析程式 | VOD +正式播放 | 不支援 |
| Moat整合 | VOD +正式播放 | Y |
| 部分廣告插播插入 | 即時 | Y |

| 功能 | 內容類型 | HLS |
|---|---|---|
| AES加密 | VOD +正式播放 | Y |
| 示例AES加密 | VOD +正式播放 | Y |
| Token化串流 | VOD +正式播放 | Y |
| Widevine DRM | VOD +正式播放 | 僅限fMP4容器 |
| Primetime DRM | VOD +正式播放 | Y |
| 外部播放(RBOP) | VOD +正式播放 | 僅限Primetime DRM |
| 許可證輪換 | VOD +正式播放 | 僅限Primetime DRM |
| 密鑰輪換 | VOD +正式播放 | 僅限Primetime DRM |

| 功能 | 內容類型 | HLS |
|---|---|---|
| Adobe Analytics VHL整合 | VOD +正式播放 | Y |
| 帳單 | VOD +正式播放 | Y |

## 已解決的問題 {#resolved-issues}

如果解決方法與報告的問題相關聯，則顯示Zendesk引用，例如ZD#xxxx。



**Android TVSDK 3.14**

本節提供TVSDK 3.14 Android版本中已解決問題的摘要。

* ZD#46903 — 當[!UICONTROL VAST]回應中的[!UICONTROL ClickTracking]、[!UICONTROL CustomClick]或[!UICONTROL CompanionClickTracking]元素的[!UICONTROL CDATA]節點為空時，應用程式當機。

### 已解決舊版中的問題

**Android TVSDK 3.12**

* ZD#40584 - Primetime參考應用程式不會使用最新的Gradle版本建置。

**Android TVSDK 3.11**

* ZD#41252 - WebVTT中的韓文字元在Android 7.1後損毀。

**Android TVSDK 3.10**

* ZD#40340 — 在列出所有TS(TypeScript)檔案的區塊之後，嘗試播放時，應用程式發生「應用程式未回應」錯誤而當機。

**Android TVSDK 3.8**

* 未新增問題。

**Android TVSDK 3.7**

* 未新增問題。

**Android TVSDK 3.6**

* 未新增問題。

**版本3.5**

* ZD#37503 — 系統會快取CRS規則的JSON回應，以避免重複要求。

**版本3.4**

* ZD#37996 — 修正線性和VOD CMAF HEVC資料流不斷播放的問題。
* ZD#37706 — 修正亂碼字幕的問題。
* ZD#37622 — 修正特定廣告的致命URISyntaxErrors問題。
* ZD#36938 — 修正位元速率在結束特技播放後，向下切換至中間位元速率，然後接至最高位元速率的問題。

**版本3.3**

* ZD#37394 - CMAF資產快速前進會在速度變更後造成偽影。
   * 修正特技播放期間設定檔變更的問題。
* ZD#37396 — 某些中段和後段廣告追蹤事件遺失。
   * 修正廣告追蹤事件的特定案例。
* ZD#37491 — 不存在帶有錯誤元的HTTP狀態代碼。
   * 已處理在堆棧中傳播較高的網路錯誤。
* ZD#37808 — 允許清單新的自定義標題。
   * 已新增SSAI_TAG支援作為此修正的一部分。
* ZD#37622 — 來自特定廣告Pod的URISyntax錯誤。
   * 修正當客戶Android應用程式收到包含未編碼%的廣告時，資料流播放當機的問題
* ZD#37631 - Android TVSDK的主資訊清單重試機制。
   * 在網路設定中新增API，以處理此增強功能。 如果未使用此API，則不會重試資訊清單。 如果已使用，則會因處理網路錯誤和逾時而重試資訊清單。

**版本3.2**

* ZD#37493 — 即時播放的追蹤信標不會針對序列中的第一個廣告間歇性觸發。
* ZD#36985- VMAP回應中的空廣告插播不會傳送追蹤信標。
* ZD#37134 - TVSDK間歇性擲回錯誤的ID以用於VMAP回應。

**版本3.0**

* ZD#33740 — 在建立MediaPlayer物件並呼叫replaceCurrentResource()後，TVSDK擲回不需要的警告

   * 改善先前的修正，僅在播放器處於暫停狀態時呼叫還原

* ZD#36442 — 每個新播放都會中斷遠端除錯工作階段，使其無法除錯。

   * 預設情況下，無法在Web檢視上進行除錯，因為預設情況下未啟用除錯。 應用程式應視需要啟用除錯，方法是對從MediaPlayer.getCustomAdView()傳回的物件呼叫setWebContentsDebuggingEnabled(true)。

* ZD#33688 — 即時支援和解決

   * 廣告插播會在廣告插播位置之前的指定間隔內解析。

* ZD#36441 — 即時視窗持續時間持續增加超過5分鐘，造成多個問題。

   * 修正在計算虛擬即時點時新增兩次virtualStartTime的問題，進而導致此問題。

**Android TVSDK 2.5.6**

* ZD #34992 — 隱藏式字幕中的語言為空。

   * 修正TVSDK未從主要資訊清單剖析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS以取得註解追蹤詳細資訊的案例。

* ZD #35078 - Android P驗證。

   * TVSDK 2.5.6已透過最新的Android P測試版組建版本進行驗證。 由於新的Android作業系統，未發現任何問題。

* ZD #34149 — 即使發生錯誤，播放器仍會繼續請求清單。

   * 修正即使所有設定檔皆關閉，TVSDK仍會重複呼叫的情況（404錯誤）。

* ZD #31533 — 在應用程式傳送至背景後，在Android上播放音訊。

   * 新增`enableAudioPlaybackInBackground` MediaPlayer的API，此API應以「True」作為引數呼叫（當播放器處於「已準備」狀態時），以在應用程式於背景時啟用音訊播放。

**Android TVSDK 2.5.5**

* ZD #21647 — 當實際視訊大小為640x360時，Android TVSDK會通知640x368。

   * 由於變數m_nOutputHeight（在AndroidMCVideoDecoder內）會以影格高度（而非實際輸出高度）更新。 在函式getVideoFrame中進行相關變更，以正確計算m_nOutputHeight。

* ZD #26614 — 緊急 — 第三方廣告服務/程式化 — 無法提供曝光數。

   * 增強先前的修正，方法是處理XML剖析中的案例，當「space」在&lt;VAST version =&quot;2.0&quot;>等於符號前時，問題可重現

* ZD #29296 - Android:新增AdSystem和創作ID至CRS請求。

   * 現在將「AdSystem」和「CreativeId」納入為1401和1403要求中的新參數。

* ZD #33062 - TVSDK在CDATA節點下的VAST回應中出現垂直號字元時當機

   * NetworkConfiguration類中的API setEncodeUrlForTracking在要編碼的URL中作為不安全字元移除

* ZD #33063 - CRS檔案選取邏輯中斷 — TVSDK未傳送CRS的webm格式要求，而是傳送給3gpp檔案。

   * 現在已修正邏輯。 使用具有webm和3gpp格式的媒體檔案時，會針對webm傳送CRS要求。 同時使用3gpp格式的媒體檔案時，會傳送最高位元速率3gpp檔案的CRS要求。

* ZD #33125 - VMAP中特定DoubleClick標籤的Android應用程式當機。

   * 修正案例以避免當機。

* ZD #32256 — 許可證輪換和密鑰輪換問題 — Adobe訪問

   * 已修正區段初始化，其中包含SampleAES內容的DRM中繼資料。 與AES128內容搭配使用即可。

* ZD #33619 — 快速轉送停滯於即時點附近緩衝狀態的播放清單內容。

   * 以特技播放模式跨越即時點時處理案例

* ZD #34151 - TimedMetadata物件順序錯誤。

   * 如果兩個TimedMetadata事件屬於時間軸中的同一時間，則會以隨機順序顯示。 在清單中維持其原始順序。

* ZD #34189 — 搜尋廣告插播開始時的問題。

   * 問題出在使用不連續性拼接的SSAI廣告。 原因是當我們開始尋找這些廣告時，我們會尋找一個關鍵幀，卻找不到它。 原因是廣告的主要音訊時間戳記早於主要視訊時間戳記。 因此，我們最終在錯誤的fragmentDump資料中搜索關鍵幀。 立即修正。

* ZD #34528 - FireTV第3代轉換器上的視頻解析度未升級到640x360以上。

   * 已增強修正功能，加入最新韌體更新

* ZD #34793 — 在某些情況下，當VideoEngine假設auditudeSettings可供使用且無法使用時，用來與自訂內容解析器當機的TVSDK 2.5.x。

   * 由於Null共用指標(auditudeSettings)上的函式呼叫，導致當機。 在VideoEngineTimeline::placeToSourceTimeline()中新增條件檢查，以在呼叫該物件上的任何項目之前，確定auditudeSettings可用。

* ZD #32584 — 無法存取VAST回應的&lt;Extensions>節點中出現的完整資訊。

   * 修正了XML剖析的相關問題，現在NetworkAdInfo提供&lt;擴充功能>節點中顯示的完整資訊

* ZD #35086 — 有特定VMAP回應時，無法從播放器取得完整的擴充功能資料。

   * 如果擴充功能xml在屬性值中有雙引號，則由於XML解析無法運作，因此此問題是擴充功能xml特有的。 修正問題。

**Android TVSDK 2.5.4**

* ZenDesk#33659 — 啟用Webview遠程調試的播放會話。

WebViewDebuging預設設定為False。 若要啟用除錯，請透過應用程式使用setWebContentsDebuggingEnabled(true)將設為true。

* ZenDesk#33011 — 如果CRS請求失敗，則無法解決廣告時間軸。

   當對廣告的CRS要求失敗時，時間軸就會解決，而剩餘的廣告會播放。

* ZenDesk#34528 - FireTV第三代轉換器的視頻解析度未升級到640x360以上。

   視訊解析度會隨著位元速率切換而提高。

* ZenDesk#33192 — 透過AudioUpdatedEventListener::onAudioUpdated擷取追蹤時，AudioTrack的名稱為null。

   在FireTV Stick上的一些情況下，當沒有實際音頻更新時，onAudioUpdate事件將被觸發。 此問題已修正。

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自訂標籤訂閱無法運作。

   我們以位元組陣列的形式（以支援APIC或一般資料）傳回ID3資料給用戶端，而在1.4中傳回字串。 位元組陣列不處理空終止字元本身，因此，它對用戶端顯示特殊字元。 此問題已修正。
* Zendesk#32670 — 播放器未故障切換至重複播放清單

   現在運作正常，且setNetworkDownVerificationUrl如預期運作。
* Zendesk#32369 — 隱藏式字幕顯示不同的顏色垃圾或工件。

   已修正最新組建版本中CC故障的問題
* Zendesk#25590 — 增強：TVSDK Cookie儲存(C++到JAVA)

   Android TVSDK現在支援在JAVA層（儲存於Android應用程式的CookieStore）和C++ TVSDK層之間存取Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎沒有PTPLAY-20269的修正

   此問題已修正，並整合至2.5.2分支。
* Zendesk#31806 - Auditude在準備中

   播放器因回應xml有空標籤而卡在準備狀態。 現在問題已修正。
* Zendesk#31727 - TVSDK 2.5隱藏式字幕字元會遭捨棄或拼字錯誤。

   問題已修正，且我們未刪除/拼寫錯誤任何字元。
* Zendesk#31485 - 2.5版DrmManager

   通過新的DrmManager（上下文）建立DrmManager時出現一些問題。 實施DRMService類，該類將提供DRMManager。
* Zendesk#32794- 1080P解析度流在Android上不播放

   我們已在2.5中更改了SizeAvailableEvent和Previsory的getHeight()和getWidth()方法，這些方法用於返回幀高和幀寬，該幀寬由媒體格式返回。 現在，它分別傳回由解碼器傳回的輸出高度和輸出寬度。
* Zendesk #19359Flash Player因設定層級資訊#EXT-X-FAXS-CM中的屬性位置而當機。

   #EXT-X-FAXS-CM標籤必須一律出現在最上層播放清單中，才會在播放清單中顯示個別位元速率或區段。

**Android TVSDK 2.5.2**

* Zendesk#17305隱藏式字幕中的非不透明背景。

   setTextFormat中的setTreatSpaceAsAlphaNum屬性被公開。 預設情況下，屬性為False。 在用戶端中將屬性設為True，以解決隱藏空間問題。

* Zendesk#25097 CC顯示帶有CC設定的視覺偽影。

   setTextFormat中的setTreatSpaceAsAlphaNum屬性被公開。 預設情況下，屬性為False。 在用戶端中將屬性設為True，以解決隱藏空間問題。

* Zendesk #31620超出TVSDK播放器的使用者代理字串遭截斷。

   128個字元後，使用者代理字串將不再截斷。

   Adobe Primetime版本字串會新增至系統使用者代理。

* Zendesk #30809缺少SEEK_END事件使應用程式無法轉換到播放狀態。
* 與先前的Primetime TVSDK版本相比，Zendesk #30415隱藏式字幕的「青色」顏色現在更深，為藍色（綠松石）。

   顏色從深青色更改為青色。

* Zendesk #30727 VOD廣告未下載/解析。

   在VMAP XML中，如果有空的VAST標籤沒有明確的結尾標籤(「&lt;/VAST>」)，且後面沒有新行字元，則VMAP XML剖析不正確，且廣告可能無法播放。

**Android TVSDK 2.5.1**

* 特定裝置(Samsung Galaxy Tab 4)當機；具有Auditude的VOD DRM LBA，然後按一下廣告。
* VHL — 從偏移處啟動內容時，會傳送錯誤的心率呼叫。
* 播放VPAID廣告時，事件:type:play廣告的VHL心率呼叫遺失。
* 進入「完成」狀態後，播放器會針對後段廣告，以SKIP adBreakPolicy回到「正在播放」狀態。
* 未將Cookie附加至傳出廣告回呼。
* 廣告提示點不可見。
* 不會載入具有獨立EAC3 SAP跟蹤的HLS。
* 當媒體播放器還原後，TVSDK接收到「螢幕開啟」目的時，播放器當機。

## 已知問題和限制 {#known-issues-and-limitations}

**Android TVSDK 3.11**

* 未新增新限制。

### 舊版的已知問題和限制

**Android TVSDK 3.10**

* 未新增新限制。

**Android TVSDK 3.8**

* 未新增新限制。

**Android TVSDK 3.7**

* 未新增新限制。

**Android TVSDK 3.6**

* 未新增新限制。

**Android TVSDK 3.5**

* 未新增限制。

**Android TVSDK 3.4**

* CMAF(CBC)資料流尚未驗證ID3、隱藏式字幕、延遲捆綁音訊支援。
* 在CMAF流上的特技播放中，由於在頂部出現視頻失真而存在重現性低的問題。

**Android TVSDK 3.3**

* CMAF資料流播放不支援clcp:c608字幕。

**Android TVSDK 3.2**

* TVSDK 3.2不支援CMAF範例AES和AES128串流播放。
* HEVC CMAF流不包括對隱藏式字幕播放的支援。
* 在非加密區段周圍執行搜尋時，WV加密資料流會顯示綠色。
* CMAF資料流不支援ID3事件。
* HLS資料流不支援TTML字幕格式。

**Android TVSDK 3.0**

* HEVC支援在此版本中有下列限制

   * 不支援DRM
   * CC(CEA 608/708)支援未驗證
   * 尚未提供4K支援
   * ID3標籤支援未驗證

* 對於廣告進度事件，時間軸列可能無法反映100%準確的廣告播放時間。 作為因應措施，您可以使用`adcompleteevent`來知道廣告播放完成，並更新UI以用於各種用途，例如更新時間軸列、移除廣告相關UI等。
* 從VMAP傳回的廣告呼叫不會遵循「及時」預覽位置。

**Android TVSDK 2.5.6**

* 不支援同時多個VMAP廣告插播。

**Android TVSDK 2.5.3**

此版本有下列問題：

* 低端裝置或不良的網路條件可能會造成即時視訊播放的音訊 — 視訊同步問題。
* 對於FER流，virtualTime和localTime可能不同。 而具有偏移的FER則無法運作。
* 搜尋延遲系結音訊內容時，播放可能卡住。
* Live內容偶爾會出現webVTT標題不同步的情況。
* 在退出廣告插播後，可看到間歇性、快速播放少量影格。
* 有時，即使播放廣告，三重包裝函式廣告插播仍會擲回303錯誤。

**Android TVSDK 2.5.2**

此版本有下列問題：

* 低端裝置上的即時視訊播放可能會發生音訊 — 視訊同步問題。
* 當搜尋至VOD媒體結尾時，播放可能會停止。
* 對於FER流，virtualTime和localTime可能不同。 此外，帶偏移的FER無法運作。

**Android TVSDK 2.5.1**

此版本的TVSDK有下列問題：

* 低端裝置上的即時視訊播放可能會發生音訊 — 視訊同步問題。
* 對於FER流，virtualTime和localTime可能不同。 此外，帶偏移的FER無法運作。
* 在VMAP XML中，如果有空的VAST標籤沒有明確的結尾標籤(&lt;/VAST>)，且後面沒有新行，則VMAP XML剖析不正確，且廣告可能無法播放。
* 不支援VPAID貼文。

## 實用資源 {#helpful-resources}

* [系統需求](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-requirements.html)
* [Android適用的TVSDK 3.10程式設計師指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-android-prog/introduction/android-3x-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API檔案](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html)  — 每個Java類別都有對應的C++類別，而C++檔案中包含的說明性資料多於Javadoc，因此請參閱C++檔案，深入了解Java API。
* [Android適用的TVSDK 1.4至2.5(Java)移轉指南](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* 有關處理螢幕開啟/關閉情況的資訊，請參閱組建中包含的`Application_Changes_for_Screen_On_Off.pdf`檔案。
* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面上的完整說明檔案。
