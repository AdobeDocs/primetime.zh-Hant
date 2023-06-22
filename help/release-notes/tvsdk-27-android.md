---
title: Android™適用的TVSDK 2.7發行說明
description: Android™適用的TVSDK 2.7發行說明說明TVSDK Android™ 2.7的新增或變更專案、已解決和已知問題以及裝置問題
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# Android™適用的TVSDK 2.7發行說明 {#tvsdk-for-android-release-notes}

Android™適用的TVSDK 2.7發行說明說明TVSDK Android™ 2.7的新增或變更專案、已解決和已知問題以及裝置問題

## TVSDK Android™ 2.7 {#tvsdk-android}

Android™參考播放器隨Android™ TVSDK包含在散發的samples/目錄中。 隨附的README&lt;.md檔案說明如何建立參考播放器。

>[!NOTE]
>
>如發行版本隨附的README.md中所述，若要成功建置參考播放器，請務必執行下列操作：
>
>1. 從下載VideoHeartbeat.jar [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (Android™ v2.0.0適用的VideoHeartbeat資料庫)
>1. 將VideoHeartbeat.jar解壓縮至libs/資料夾。

>


## 新功能 {#new-features}

適用於Android™的TVSDK 2.7包含1.4版的所有功能，但不包含下列不支援的功能 [功能矩陣](#feature-matrix).

**Android™ TVSDK 2.7**

* **平行廣告解析度支援**

TVSDK 2.7支援廣告插播中所有廣告請求的同時解析，而非循序解析。

### 舊版中的新功能 {#new-features-previous-releases}

**版本2.5.6**

* **TVSDK 2.5支援Android™ P**
* **啟用背景音訊**

   若要在應用程式從前景移至背景時啟用音訊播放，當播放器處於「已準備」狀態時，應用程式應呼叫具有true作為引數的MediaPlayer的enableAudioPlaybackInBackground API。

* **MediaPlayer類別中的alwaysUseAudioOutputLatency（布林值）**

設定後，請在音訊時間戳記計算中使用輸出延遲。
布林值引數val - True在音訊時間戳記計算中使用音訊輸出延遲。

* **最佳化，即使頻寬速度突然下降，也能提供最佳播放體驗。**
TVSDK現在會視需要取消進行中的區段下載，並動態切換至適當的轉譯。 這是透過順暢切換位元速率而不中斷來完成。

**版本2.5.5**

* **部分廣告插播插入**

   在廣告中間加入，而不引發部分觀看廣告追蹤的電視體驗。\
   範例：使用者在包含三個30秒廣告的90秒廣告插播中間（在40秒）加入。 這是插播中第二個廣告的10秒。
   * 第二個廣告會播放剩餘的持續時間（20秒），接著是第三個廣告。
   * 部分已播放廣告（第二個廣告）的廣告追蹤器未觸發。 只會觸發第三個廣告的追蹤器。

* **安全透過HTTPS載入廣告**

   Adobe Primetime提供可透過https要求第一次呼叫primetime廣告伺服器和CRS的選項。

* **CRS請求中新增的AdSystem和Creative ID**

   * 現在包含 `AdSystem` 和 `CreativeId` 做為1401和1403要求中的新引數。

* **NetworkConfiguration類別中的API setEncodeUrlForTracking已移除** 因為URL中的不安全字元應經過編碼。

**版本2.5.4**

Android™ TVSDK v2.5.4提供下列更新和API變更：

* 預設值的變更 `WebViewDebbuging`

   此 `WebViewDebbuging` 值設定為 _False_ 依預設。 若要啟用，請呼叫 `setWebContentsDebuggingEnabled` 至 _True_ 應用程式中。

* OpenSSL和Curl版本升級已更新 `libcurl` 至v7.57.0和OpenSSL至v1.0.2k。
* VAST回應物件的應用程式層級存取引進了新的API NetworkAdInfo：：getVastXml()，可讓您存取應用程式的VAST回應物件。

**版本2.5.3**

Android™ TVSDK v2.5.3提供下列更新和API變更。

* 鼓勵所有使用CRS的TVSDK客戶透過TVSDK 2.5.3.85或Android™最新版本升級應用程式。 這是現有應用程式實作的下拉式替代專案。 TVSDK升級後，請在Proxy工具（例如：Charles）中檢查CRS創意URL請求，並確認路徑中的主機名稱和版本反映為如以下範例URL結構中所示。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK的使用者代理程式可自訂：我們已新增一些新的API來自訂使用者代理。

   * `setCustomUserAgent`（字串值）
   * `getCustomUserAgent`()

* 在Android™應用程式和TVSDK之間共用Cookie： Android™ TVSDK現在支援在Java™層(儲存在Android™應用程式的CookieStore中)和C++ TVSDK層之間存取Cookie。 現在，您可以在原生C++層中設定及/或修改Cookie，因為它們會公開至Java™ Cookie Store。
* API變更：

   * 已新增事件CookieUpdatedEvent。 當媒體播放器的Cookie更新時，媒體播放器會傳送此訊息。
   * 新API已新增至 `NetworkConfiguration::set/ getCustomUserAgent()` 以使用自訂使用者代理。
   * 新API已新增至 `NetworkConfiguration::set/ getEncodedUrlForTracking` 以強制編碼不安全的字元。
   * 新API已新增至 `NetworkConfiguration::getNetworkDownVerificationUrl()` 設定網路驗證URL （如果發生容錯移轉）。
   * TextFormat：：treatSpaceAsAlphaNum新增屬性，定義顯示註解時是否將空格視為英數字元。

* 中的變更 `SizeAvailableEvent`：先前的getHeight()和getWidth()方法 `SizeAvailableEvent` 在2.5.2中，用來傳回由媒體格式傳回的影格高度和影格寬度。 現在，它會分別傳回解碼器傳回的輸出高度和輸出寬度。
* 緩衝行為的變更：緩衝行為已變更。 由應用程式開發人員自行決定緩衝為空時該怎麼做。 2.5.3在緩衝區空白的情況下使用播放緩衝區大小。

**版本2.5.2**

Android™ TVSDK v2.5.2提供重要的錯誤修正和一些API變更。

**版本2.5.1**

Android™ 2.5.1版的重要新功能。

* **效能改良**&#x200B;新的TVSDK 2.5.1架構提供數項效能改善。 根據協力廠商基準測試研究的統計資料，新架構的啟動時間比業界平均水準縮短5倍，掉格數減少3.8倍：

   * **立即開啟VOD和即時 —** 當您啟用立即開啟時，TVSDK會在播放開始之前初始化並緩衝媒體。 由於您可以在背景同時啟動多個MediaPlayerItemLoader執行個體，因此您可以緩衝多個串流。 當使用者變更頻道，並且資料流已正確緩衝時，新頻道上的播放會立即開始。 TVSDK 2.5.1也支援以下專案的立即開啟： **live** 串流也會。 即時視窗移動時，即時資料流會遭到緩衝。

      * **改善ABR邏輯 —** 新的ABR邏輯是以緩衝區長度、緩衝區長度變更速率和測量到的頻寬為基礎。 這可確保ABR在頻寬波動時選擇正確的位元速率，並透過監控緩衝區長度變更的速率，最佳化位元速率切換的實際發生次數。
      * **部分割槽段下載/細分 —** TVSDK進一步縮小每個片段的大小，以儘快開始播放。 ts片段必須每兩秒有一個關鍵影格。
      * **延遲廣告解析度 —** TVSDK不會等到非前段廣告解決後再開始播放，因此縮短了啟動時間。 除非解決所有廣告，否則仍不允許搜尋和特技播放等API。 這適用於與CSAI搭配使用的VOD資料流。 在完成廣告解析之前，不允許搜尋和快速前進等操作。 對於直播串流，此功能無法在直播活動期間啟用廣告解析功能。
      * **持續性網路連線 —** 此功能可讓TVSDK建立並儲存持續性網路連線的內部清單。 這些連線會重複用於多個請求，而不是為每個網路請求開啟新的連線，然後將其銷毀。 這會提高網路程式碼的效率並減少延遲，進而加快播放效能。
TVSDK開啟連線時，會要求伺服器輸入 *保持連線* 連線。 有些伺服器可能不支援這種連線，在這種情況下TVSDK會退回重新為每個要求建立連線。 此外，雖然持續連線預設為開啟，但TVSDK現在提供設定選項，讓應用程式可視需要關閉持續連線。
      * **平行下載 —** 同時下載視訊與音訊而非串列下載，可減少啟動延遲。 此功能可播放HLS Live和VOD檔案、最佳化伺服器的可用頻寬使用量、降低進入緩衝區執行不足的機率，以及將下載和播放之間的延遲降至最低。
      * **平行廣告下載 —** TVSDK會在點選廣告插播前，與內容播放同時預先擷取廣告，因此可順暢地播放廣告和內容。

* **播放**

   * **MP4內容播放 —** MP4短片不需要重新轉碼，就能在TVSDK中播放。
注意：MP4播放不支援ABR切換、特技播放、廣告插入、延遲音訊繫結和子區段。
   * **使用最適化位元速率(ABR)的特技播放 —** 此功能可讓TVSDK在特技播放模式中切換iFrame資料流。 您可以使用非iFrame設定檔，以較慢的速度進行特技播放。
   * **更流暢的戲法遊戲 —** 這些改善專案可增強使用者體驗：

          *根據頻寬和緩衝設定檔，在特技播放期間選擇最適化位元速率和影格速率
          *使用主要資料流而不是IDR資料流，以取得最高30 fps的快速播放。
      
* **內容保護**

   * **以解析度為基礎的輸出保護 —** 此功能將播放限制繫結至特定解析度，提供更精細的DRM控制項。

* **工作流程支援**

   * **直接帳單整合 —** 這會將計費量度傳送至Adobe Analytics後端，該後端經Adobe Primetime針對客戶使用的資料流認證。
TVSDK會根據客戶銷售合約自動收集量度，以產生開立帳單所需的定期使用報告。 在每個資料流開始事件上，TVSDK會使用Adobe Analytics資料插入API來傳送計費量度，例如內容型別、啟用廣告插入的旗標及啟用drm的旗標（根據可計費資料流的持續時間）至Adobe Analytics Primetime擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 系統會根據要求定期傳送此計費使用情況報告給客戶。 這是計費功能的第一個階段，僅支援使用計費。 您可以使用檔案中描述的API，根據銷售合約進行設定。 此功能預設為啟用。 若要關閉此功能，請參閱參考播放器範例。
   * **改善容錯移轉支援 —** 即使主機伺服器、播放清單檔案和區段失敗，仍實施其他策略以繼續不間斷播放。

* **廣告**

   * **Moat整合 —** 支援來自Moat的廣告可見度測量。
   * **隨附橫幅 —** 隨附橫幅會與線性廣告一併顯示，且通常在廣告結束後繼續顯示在檢視上。 這些橫幅可能是html型別(HTML片段)或iframe型別（iframe頁面的URL）。

* **分析**

   * **VHL 2.0 -** 這是最新最佳化的視訊心率程式庫(VHL)整合，可自動收集Adobe Analytics的使用量資料。 API的複雜度已降低，以方便實作。 下載VHL程式庫 [適用於Android™的v2.0.0](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) 並解壓縮libs資料夾中的JAR檔案。

* **SizeAvaliableEventListener**
   * SizeAvailableEvent的getHeight()和getWidth()方法現在將分別傳回高度和寬度的輸出。 顯示外觀比例的計算方式如下：

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookie**

   * Android™ TVSDK現在支援存取Android™應用程式CookieStore中儲存的Java™ Cookie。 每當新的Cookie成為「Set-Cookie」回應標頭的一部分時，就會提供回呼API (onCookiesUpdated)加以記錄。 透過CookieStore在特定URI/網域上設定這些Cookie值，可將這些Cookie作為用於不同URI/網域的HttpCookie清單使用。 同樣地，TVSDK中的Cookie值也是使用CookieStore add API來更新。

## 功能矩陣 {#feature-matrix}

Android™適用的TVSDK支援多種功能，您可實施這些功能來將功能新增至視訊應用程式。

在下列功能表中，「Y」表示目前版本支援該功能。

| 功能 | 內容型別 | HLS |
|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD +即時 | Y |
| FER — 一般播放（播放、暫停、搜尋） | FER VOD | Y |
| 在廣告播放時搜尋 | VOD +即時 | 不支援 |
| AC3 | VOD +即時 | 不支援 |
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
| 設定最適化位元速率控制項 | VOD +即時 | Y |
| 自訂資訊清單標籤 | VOD +即時 | Y |
| 延遲音訊繫結 | VOD +即時 | Y |
| 302重新導向 | VOD +即時 | Y |
| 有位移的播放 | VOD +即時 | Y |
| 僅限音訊播放 | VOD +即時 | Y |
| 特技播放 | VOD +即時 | Y |
| 戲法遊戲中的慢動作 | VOD +即時 | 不支援 |
| Smooth Trick Play （使用ABR） | VOD +即時 | Y |
| ID3剖析 | VOD +即時 | Y |
| 廣告中斷 | VOD +即時 | 不支援 |
| 立即開啟 | VOD +即時 | 不支援 |
| 不連續標籤支援 | VOD +即時 | Y |
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
| 延遲廣告解決 | VOD | Y |
| 不連續標籤支援 — SSAI | VOD +即時 | Y |
| 隨附廣告、橫幅廣告和可點按廣告 | VOD +即時 | Y |
| VPAID 2.0 | VOD +即時 | Y (JS) |
| 早期廣告退出 | 即時 | Y |
| 規則型創意優先順序 | VOD +即時 | Y |
| CRS規則 | VOD +即時 | Y |
| JSON Ad Resolver | VOD +即時 | 不支援 |
| Moat整合 | VOD +即時 | Y |

| 功能 | 內容型別 | HLS |
|---|---|---|
| AES加密 | VOD +即時 | Y |
| AES加密範例 | VOD +即時 | Y |
| 代碼化的資料流 | VOD +即時 | Y |
| DRM | VOD +即時 | 僅限Primetime DRM （未來：Widevine） |
| 外部播放(RBOP) | VOD +即時 | 僅限Primetime DRM |
| 授權輪換 | VOD +即時 | 僅限Primetime DRM |
| 金鑰輪換 | VOD +即時 | 僅限Primetime DRM |

| 功能 | 內容型別 | HLS |
|---|---|---|
| Adobe Analytics VHL整合 | VOD +即時 | Y |
| 帳單 | VOD +即時 | Y |

## 已解決的問題 {#resolved-issues}

如果解決方法與報告的問題相關聯，則會顯示Zendesk參考，例如ZD#xxxxx

**Android™ TVSDK 2.7**

本節提供TVSDK 2.7版本中已解決的問題摘要。

* ZD#37166 — 即使廣告播放正常，也會觸發錯誤追蹤呼叫。
* ZD#37134 — 傳回錯誤的廣告ID，以防包裝函式(3P)廣告在VMAP回應中出現多個廣告。

**Android™ TVSDK 2.5.6**

* ZD #34992 — 隱藏式字幕中的語言是空的。
   * 修正TVSDK未從主要資訊清單剖析#EXT-X-MEDIA：TYPE=CLOSED-CAPTIONS以取得標題追蹤詳細資料的情況。
* ZD #35078 - Android P驗證。
   * TVSDK 2..5.6已透過最新Android™ P測試版組建進行驗證。 由於新的Android™作業系統，找不到任何問題。
* ZD #34149 — 即使發生錯誤，播放器仍會繼續要求資訊清單。
   * 修正TVSDK進行重複呼叫的情況，即使所有設定檔都已關閉（404錯誤）。
* ZD #31533 — 在應用程式傳送至背景後，在Android™上播放音訊。
   * 已新增 `enableAudioPlaybackInBackground` MediaPlayer的API，此類API應以「True」作為引數來呼叫（當播放器處於「已準備」狀態時），以便在應用程式於背景時啟用音訊播放。

**Android™ TVSDK 2.5.5**

* ZD #21647 - Android TVSDK會在實際視訊大小為640x360時通知640x368。
   * 由於變數m_nOutputHeight （在AndroidMCVideoDecoder內）會以影格高度而非實際輸出高度更新。 在函式getVideoFrame中進行相關變更，以正確計算m_nOutputHeight。
* ZD #26614 — 緊急 — 第三方廣告服務/程式化 — 未能提供曝光數。
   * 透過處理XML剖析中的案例，加強之前的修正，此問題可在「space」位於「equal」符號（例如）之前時重現 &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android：將AdSystem和Creative ID新增至CRS請求。
   * 現在在1401和1403請求中包含&#39;AdSystem&#39;和&#39;CreativeId&#39;作為新引數。
* ZD #33062 - TVSDK在CDATA節點下的VAST回應中發生垂直號字元時當機
   * NetworkConfiguration類別中的API setEncodeUrlForTracking已移除，成為要編碼之URL中的不安全字元。
* ZD #33063 - CRS檔案選擇邏輯損毀 — TVSDK未傳送webm格式的CRS請求，而是改為傳送3gpp檔案的請求。
   * 現在已修正邏輯。 在搭配webm和3gpp格式使用媒體檔案時，會要求為webm傳送CRS。 而且在使用具有3gpp格式的兩個媒體檔案時，會針對最高位元速率3gpp檔案傳送CRS請求。
* ZD #33125 - Android應用程式當機，且VMAP中有特定的DoubleClick標籤。
   * 修正此情況以避免當機。
* ZD #32256 — 授權輪換和金鑰輪換問題 — Adobe存取。
   * 修正SampleAES內容使用DRM中繼資料進行區段初始化的問題。 適用於AES128內容。
* ZD #33619 — 快速轉送在即時點附近陷入緩衝狀態的成長中播放清單內容。
   * 處理在特技播放模式中跨過即時點時的情況。
* ZD #34151 - TimedMetadata物件順序錯誤。
   * 兩個TimedMetadata事件如果屬於時間軸中的同一時間，則會以隨機順序出現。 維持資訊清單中的原始順序。
* ZD #34189 — 搜尋廣告插播開始時發生問題。
   * 該問題與使用不連續拼接的SSAI廣告有關。 原因是當我們尋找這類廣告的開頭時，我們尋找關鍵影格，卻找不到關鍵影格。 原因是廣告的最小音訊時間戳記在最小視訊時間戳記之前。 因此，我們最終會在錯誤的fragmentDump資料中搜尋關鍵框架。 現已修正。
* ZD #34528 — 在FireTV第三代硬體鎖上，視訊解析度不可升級至640x360以上。
   * 增強修正功能，加入最新的韌體更新。
* ZD #34793 — 有時VideoEngine假設auditudeSettings可用但未使用時，TVSDK 2.5.x會與自訂內容解析程式當機。
   * 當機的發生是因為在Null共用指標(auditudeSettings)上呼叫函式。 在VideoEngineTimeline：：placeToSourceTimeline()中新增條件檢查，以確保在呼叫該物件上的任何內容之前，auditudeSettings都可供使用。
* ZD #32584 — 無法存取 &lt;extensions> vast回應的節點。
   * 已修正有關XML剖析的問題，現在NetworkAdInfo提供 &lt;extensions> 節點。
* ZD #35086 — 如果有特定VMAP回應，則無法從播放器取得完整的擴充功能資料。
   * 此問題特定於擴充功能xml，因為如果擴充功能xml在屬性值內有雙引號，則XML剖析無法運作。 已修正問題。

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 — 啟用Webview遠端偵錯的播放工作階段。
   * WebViewDebugging預設為False。 若要啟用偵錯，請使用setWebContentsDebuggingEnabled(true)，透過應用程式設定為true。
* ZenDesk#33011 — 如果存在失敗的CRS請求，則不會解析廣告時間表。
   * 當對廣告的CRS請求失敗時，時間軸會解析並播放其餘廣告。
* ZenDesk#34528 — 在FireTV第三代硬體鎖上，視訊解析度無法升級至640x360以上。
   * 視訊解析度會隨著位元速率切換而提高。
* ZenDesk#33192 — 透過AudioUpdatedEventListener：：onAudioUpdated擷取曲目時，AudioTrack的名稱為空。
   * 在FireTV Stick的少數案例中，在沒有實際音訊更新時，就會觸發onAudioUpdate事件。 此問題已修正。

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自訂標籤訂閱無法運作。
   * 我們將ID3資料以位元組陣列（以支援APIC或一般資料）傳回給使用者端，而傳回1.4字串中的資料。 位元組陣列本身不處理Null終止字元，因此會向使用者端顯示特殊字元。 此問題現已修正。
* Zendesk#32670 — 播放器未容錯移轉至備援播放清單
   * 現在此功能正常，setNetworkDownVerificationUrl可如預期運作。
* Zendesk#32369 — 隱藏式字幕顯示不同的顏色垃圾或成品。
   * CC問題已在最新組建版本中修正
* Zendesk#25590 — 增強功能：TVSDK Cookie存放區(C++至Java™)
   * Android™ TVSDK現在支援存取Java™層(儲存在Android™應用程式的CookieStore中)與C++ TVSDK層之間的Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎沒有PTPLAY-20269的修正。此問題已修正並整合至2.5.2分支。
* Zendesk#31806 - PREPARING Player中的Auditude杆卡在Preparing狀態，因為回應xml有空白標籤。 問題已修正。
* Zendesk#31727 - TVSDK 2.5隱藏式字幕字元遭到捨棄或拼錯字。
   * 問題已修正，且我們不會捨棄/拼錯任何字元。
* Zendesk#31485 - DrmManager 2.5版
   * 透過新的DrmManager（前後關聯前後關聯）建立DrmManager時發生一些問題。 實作DRMService類別，提供DRMManager。
* Zendesk#32794 — 無法在Android™上播放1080P解析度資料流。
   * 我們已變更SizeAvailableEvent。 先前， `getHeight()` 和 `getWidth()` 2.5中的SizeAvailableEvent方法，用來傳回媒體格式所傳回的影格高度和影格寬度。 現在，它會分別傳回解碼器傳回的輸出高度和輸出寬度。
* Zendesk #19359Flash Player會因為#EXT-X-FAXS-CM屬性在設定層級資訊清單中的位置而當機。
   * 在個別位元速率或區段出現於播放清單之前，#EXT-X-FAXS-CM標籤必須一律出現於最上層播放清單。

**Android™ TVSDK 2.5.2**

* Zendesk#17305具有非不透明背景的隱藏式字幕中的不自然感。
TextFormat中的setTreatSpaceAsAlphaNum屬性會公開。 依預設，屬性為False。 在使用者端中將屬性設定為True以解決深色空格問題。

* Zendesk#25097 CC display具有CC設定的視覺成品。
TextFormat中的setTreatSpaceAsAlphaNum屬性會公開。 依預設，屬性為False。 在使用者端中將屬性設定為True以解決深色空格問題。

* 傳出TVSDK播放器的Zendesk #31620使用者代理字串被截斷。
128個字元後，使用者代理字串將不再被截斷。
Adobe Primetime版本字串已新增至系統使用者代理。

* Zendesk #30809遺失SEEK_END事件會使應用程式無法轉換為播放狀態。
* 與舊版Primetime TVSDK相比，Zendesk #30415隱藏式字幕的「青色」顏色現在為較暗的藍色（藍綠色）。

   顏色從深青色變更為青色。

* 未下載/解析Zendesk #30727 VOD廣告。

   在VMAP XML中，如果存在沒有明確結尾標籤(&#39;的空VAST標籤&lt;/vast>&#39;)且後面沒有新行字元，則VMAP XML無法正確剖析，且可能無法播放廣告。

**Android™ TVSDK 2.5.1**

* 裝置特定(Samsung Galaxy Tab 4)當機；具有Auditude的VOD DRM LBA並按一下廣告。
* VHL — 從位移開始內容時，傳送不正確的心率呼叫。
* 播放VPAID廣告時，VHL心率會呼叫事件:type:播放廣告遺失。
* 進入「完成」狀態後，播放器會針對後置廣告返回到「正在播放」狀態並顯示「略過adBreakPolicy」。
* Cookie未附加至傳出廣告回呼。
* 廣告提示點不可見。
* 無法載入具有獨立EAC3 SAP磁軌的HLS。
* 媒體播放器還原後，TVSDK收到Screen On意圖，導致播放器當機。

## 已知問題和限制 {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7最多可支援5個廣告的並行解析度。
* 若是VMAP回應，單一廣告插播中的廣告呼叫會同時發生，而廣告插播會依序解決。
* 在FER的情況下，會同時解析每個機會中的廣告呼叫。

### 舊版中的已知問題和限制{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* 不支援同時有多個VMAP廣告插播。

**Android™ TVSDK 2.5.3**

此版本有以下問題：

* 即時視訊播放在低端裝置或不良網路狀況下可能有音訊 — 視訊同步問題。
* 對於FER資料流，virtualTime和localTime可能會有所不同。 此外，具有位移的FER也不起作用。
* 搜尋延遲繫結音訊內容時，播放可能會卡住。
* LIVE內容的webVTT字幕可能會間歇性地失去同步。
* 在結束廣告插播後，可以間歇性地快速播放幾個畫面。
* 有時候，即使播放了廣告，也會對三個包裝函式廣告插播擲回303錯誤。

**Android™ TVSDK 2.5.2**

此版本有以下問題：

* 低端裝置上的即時視訊播放可能有音訊 — 視訊同步問題。
* 搜尋至VOD媒體結尾時，播放可能會在某些時間停止。
* 對於FER資料流，virtualTime和localTime可能會有所不同。 此外，具有位移的FER也不起作用。

**Android™ TVSDK 2.5.1**

此版本的TVSDK有下列問題：

* 低端裝置上的即時視訊播放可能有音訊 — 視訊同步問題。
* 對於FER資料流，virtualTime和localTime可能會有所不同。 此外，具有位移的FER也不起作用。
* 在VMAP XML中，如果存在沒有明確結尾標籤的空白VAST標籤(&lt;/vast>)，且後面沒有新行，則VMAP XML無法正確剖析，且廣告可能無法播放。
* 不支援VPAID後置滾動。

## 實用資源 {#helpful-resources}

* [系統需求](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [Android™適用的TVSDK 2.7程式設計師指南](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [TVSDK Android™ Javadoc for API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android™ C++ API檔案](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  — 每個Java™類別都有對應的C++類別，且C++檔案包含的說明資料比Java™檔案更多，因此請參考C++檔案，深入瞭解Java™ API。
* [TVSDK 1.4至2.5 for Android™ (Java™)移轉指南](/help/migration-guides/tvsdk-14-25-android.md)
* 如需處理熒幕開啟/關閉的情況，請參閱 `Application_Changes_for_Screen_On_Off.pdf` 組建中包含的檔案。
* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://experienceleague.adobe.com/docs/primetime.html) 頁面。
