---
title: 適用於案頭HLS的TVSDK 1.4發行說明
description: 案頭HLS適用的TVSDK發行說明說明TVSDK DHLS的新增或變更專案、已解決的問題及已知問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5194'
ht-degree: 0%

---

# 適用於案頭HLS的TVSDK 1.4發行說明 {#tvsdk-for-desktop-hls-release-notes}

Desktop HLS適用的TVSDK發行說明說明，說明TVSDK DHLS的新增或變更專案、已解決問題和已知問題。

## 新功能 {#new-features}

**1.4.31**

* **CRS廣告的多CDN支援**

   * 依預設，所有轉碼資產都會在Akamai上的Adobe擁有的CDN上託管。 在最新版本中，Adobe Creative Repackaging Service (CRS)提供將轉碼創意內容上傳到客戶指定的多個CDN的功能。
   * 新的API會新增至TVSDK，以便在不使用預設URL時指定最終CRS創意URL。 請參閱檔案以瞭解如何使用這些新API。

### 舊版中的新功能 {#new-features-previous}

**1.4.30**

* **計費量度**

為因應客戶只想依使用量付款，而不論實際使用量為何，Adobe會收集使用量度，並使用這些量度來決定向客戶收費的金額。

**1.4.24**

* **持續性網路連線**

重要：您必須至少安裝AdobeFlash Player版本22或更新版本。
持續性網路連線會建立並儲存可重複用於多個要求的網路連線內部清單，而不是為每個網路要求開啟新連線。 持續性的網路連線應該會提高效率，並減少網路程式碼中的延遲。

在這個版本中，Mac上的Apple Safari和Mozilla Firefox不支援此功能。

**1.4.19**

* VPAID廣告的串流完整性支援。
* 已修正擱置問題，在Firefox 42和更新版本的Flash播放器FP 20.0.0.267中啟用「靜音」索引標籤選項。

**1.4.18**

* Primetime Desktop HLS TVSDK現在支援VPAID 2.0線性SWF創意，以提供豐富的互動式串流廣告體驗。

**1.4.10**

* **廣告遞補、廣告選擇邏輯中的Daisy鏈結(Zendesk #3103)** 對於已啟用遞補規則的VAST廣告（創意內容），TVSDK會將具有無效MIME型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

如需詳細資訊，請參閱 [VAST和VMAP廣告的廣告遞補](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **視訊心率程式庫(VHL)更新至1.5版**

   * 能夠連同視訊開始和/或視訊/廣告/章節開始一起傳送中繼資料作為內容資料
   * 網路流量較少 — 心率平均而言更少，且大小更小。

**1.4.7**

* **內部部署個人化支援**

支援Adobe個人化伺服器的內部部署安裝，可自訂使用者端的個人化請求，以移至其他端點。

**1.4.6**

* **範例AES加密(需要Flash Player版本17.0.0.134)**

現在支援以範例為基礎的AES加密。

**1.4.2**

* **視訊心率程式庫(VHL)更新至1.4.0.1版**

   * 新增將其他SDK或播放器中的不同分析使用案例與Adobe Analytics Video Essentials搭配的功能。
   * 已透過移除trackAdBreakStart和trackAdBreakComplete方法來最佳化廣告追蹤。 從trackAdStart和trackAdComplete方法呼叫推斷廣告插播。
   * 追蹤廣告時不再需要播放點屬性。

**1.4.0**

* **透過替代內容取代發出中斷訊號** 在1.4 TVSDK更新中，TVSDK現在也支援針對線性內容進入和從區域中斷返回。 TVSDK現在可以平行處理兩個資訊清單檔案（主要和替代），以監視中斷訊號，即使替代程式設計正在取代原始程式設計時也是如此。

* **移除/取代C3廣告** 現在，不需要進行額外的準備工作，即可將新廣告動態插入即將從C3視窗中出來的隨選影片(VOD)資產。 TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 在廣播期間播放即時/線性內容，而且會立即下拉以供隨選內容使用（沒有適當的時間來「清除」資產）的情況下，這項強大的新功能也相當實用。

## 已解決問題 {#resolved-issues}

>[!NOTE]
>
>強烈建議所有使用CRS的TVSDK客戶在iOS、Android和案頭HLS上至少升級為TVSDK 1.4.32。 此升級會取代現有的應用程式實作。 升級後，在Proxy工具（例如Charles）中檢查CRS創意URL請求，驗證路徑中的版本是否反映3.1版。例如，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**1.4.41版**

* Zendesk #33777 - DHLS散發組建的Localhost權杖SWF已過期。

  正在更新DHLS上PMP示範的localhost權杖。

### 舊版中的已解決問題 {#resolved-issues-previous}

**版本1.4.38** (891)

* Zendesk #30731 - TVSDK不會在AdBreak中播放多個VPAID廣告。

  修正AdBreak中多個VPAID廣告播放的問題。

* Zendesk #29968 — 雙人告示板。

  視訊播放器可在發生ABR切換時，重複該時段的最後一個區段。 因此，有時候會重複上一個前置區段。 此問題已修正。

**版本1.4.35** (879)

* Zendesk #26058 — 支援原生VPAID事件

**版本1.4.33** (873)

* Zendesk #21701 — 傳送1401 CRS請求的原始創意URL，而不是標準化的URL。

  已根據CRS後端要求，修正要求重新封裝URL進行轉碼的問題。
* Zendesk #26197 — 未以所需的顯示解析度重播變形壓縮。

  **注意**：此問題需要Flash播放器24.0.0.194或更新版本。

  已修正使用外觀比例表格中的遺失專案計算輸出寬度的問題。

* Zendesk #26840 — 第二次嘗試後，IE11 + Windows7上的HDCP偵測失敗。

  **注意**：此問題需要Flash播放器24.0.0.218或更新版本。

  此問題已藉由修改AdobeCP的主要訊息佇列處理來解決，以便在整個佇列進行反複處理，而不只是封鎖第一則訊息。

* Zendesk #27460 — 新的Akamai帳戶無法處理POST CDN請求。

  新的CDN帳戶無法處理POST CDN請求。 此問題已透過更新程式碼以使cdn.auditude.com廣告請求成為GET而非POST來解決。
* Zendesk #27619 - Windows 10上的Flash當機

  **注意**：此問題需要Flash播放器24.0.0.218或更新版本。

  此問題已藉由防止長URL造成的錯誤而解決。

* Zendesk #28218 — 從恢復點回撥時，不會觸發追蹤事件

  此問題與Zendesk #26592中的問題相同。 已修正當媒體播放器處於VOD資料流的「已準備」狀態時允許搜尋作業的問題。

**版本1.4.32** (867)

* Zendesk #26592追蹤事件不會在播放從恢復點開始時引發

當繼續點不是零時，程式碼沒有更新前段廣告插播專案。 此問題已透過新增邏輯以在範圍開始時間不符時重新整理程式碼來解決。

* Zendesk #27022廣告沒有在第二次播放資產時播放

已修正陣列方法的例外狀況。

**1.4.30版** (855)

此版本中TVSDK的下列問題已解決：

* Zendesk #22898 — 缺少字幕不應導致播放失敗。

**注意**：此問題需要Flash播放器23.0.0.185或更新版本。

即使資訊清單遺失WebVTT M3U8，但允許TVSDK繼續播放，且僅註冊警告，此問題已解決。

* Zendesk #23454 — 無法正確處理協力廠商廣告(VPAID)

根據內容ID而非時間範圍，正確處理VPAID廣告即可解決此問題。

* Zendesk #24528 — 計費的TVSDK使用量度。

重要：此問題需要Flash播放器23.0.0.185或更新版本。

* Zendesk # 25432調整播放器大小時出現隱藏式字幕問題。

重要：此問題需要Flash播放器23.0.0.185或更新版本。

註解顯示紋理對應程式碼已固定，可在播放器調整大小期間正確處理座標。

視訊心率程式庫(VHL)已更新至1.5.9版，以解決下列問題：

* Zendesk #23730 — 位元速率量度是空的

此問題已藉由追蹤VideoAnalyticsTracker中的位元速率變更而解決。

* 在PTVideoAnalyticsTrackingMetadata中新增API assetDuration，以更新即時/線性資料流的資產持續時間。

**版本1.4.28** (848)

* Zendesk #25027 -Auditude在1.4.27案頭版中無法運作

此問題已透過新增代碼以檢查AUDITUDE_METADATA_KEY以及使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互換而解決。

* Zendesk #24428 — 使用TVSDK播放DRM HLS時經常出現緩衝問題

當沒有廣告設定時，TVSDK可消除專為同步廣告插入而設計的時間表上的前段廣告保留和即時保留保留，以加快處理速度，此問題已獲得解決。

* Zendesk #24344 — 停用WebVTT檔案以縮短啟動時間。

**注意**：此問題需要Flash播放器23或更新版本。

此問題已透過載入WebVTT檔案解決，但僅限需要顯示註解時。

* Zendesk #24994 — 從商業休假返回時，隱藏式字幕會從播放器上掉下來

**注意**：此問題需要Flash播放器23或更新版本。

虛假的EOC程式碼導致註解顯示消失。 此問題已透過強制608字幕代碼RU2、RU3和RU4在目前使用中視窗中提供正確的可見度來解決。

**版本1.4.27** (844)

* Zendesk #21554 — 未針對application-type = video/mp4觸發TVSDK錯誤信標

啟用TVSDK以偵測無效資產格式上的正確錯誤追蹤URL，即可解決此問題。

* Zendesk #23402 — 不完整的廣告播放

**注意**：此問題需要Flash播放器23或更新版本。

在某些要求上收到404錯誤之後，可能會發生當機。 此問題已透過確保連線在處理回應時不會關閉而解決。 解決方法可確保VPAID廣告檔案不會被錯誤計數，所以在下載時不會被釋放。

* Zendesk #23621 — 在400和404上重試失敗

**注意**：此問題需要Flash播放器23或更新版本。

修正在不同設定檔之間切換時，造成DRM中繼資料損毀的問題。

* Zendesk #23705 — 廣告拼接插播期間影片廣告凍結

**注意**：此問題需要Flash播放器23或更新版本。

此問題與Zendesk #23621中的問題相同。

* Zendesk #23905 — 廣告插播會略過某些廣告插播

**注意**：此問題需要Flash播放器23或更新版本。

Windows原生網路程式碼已修正，以確保連線不會關閉其他連線目前正在使用的控制代碼。

* 票證#24029 - HLS FER資料流不會播放中段.json檔案中的所有中段廣告。

此問題已透過允許使用者端在Opportunity執行個體上個別設定自訂引數來解決，因此使用者端不必覆寫OpportunityGenerator。

**版本1.4.26** (839)

* Zendesk #18854 — 根據CRS規則更新創意選擇邏輯
   * 支援根據CRS規則更新創意選擇邏輯

* Zendesk #22725 — 案頭範例應用程式中的playbackManager.beginPlayback()實作

   * 已透過在startPlaybackFromFlashVars結尾移除此備援呼叫來修正，因為此方法是從setupVideo()呼叫

* Zendesk #22807 - SeekManager Null參考例外狀況

   * 已藉由在SeekManager內提供與_dispatcher相關的必要NULL指標保護來修正

* Zendesk #22822 — 使用TVSDK播放清晰HLS時頻繁緩衝

   * 若沒有廣告，移除由adSignalingModeOpportunityGenerator產生的初始機會即可修正

* Zendesk #23378 — 資料流完整性封鎖rules.xml

   * 透過串流完整性工作流程載入rules.xml檔案來修正

**版本1.4.24** (817)

* Zendesk #19851 — 當播放器適應不同的位元速率時，會在新的位元速率上跳回幾個時間格，造成尷尬的體驗

**注意**：此問題需要Flash播放器22.0.0.175或更新版本。

已解決DRM介面卡在下載區段的一小部分後無法正確還原的問題。

* Zendesk #20784 - Analytics：觸發即時視訊轉換的內容完成

此問題已藉由新增API (trackVideoComplete)在LINEAR/LIVE視訊追蹤工作階段期間手動觸發內容完成來解決。

下列程式庫已更新：

* Zendesk #21643 - VPAID廣告不會完整播放

   * AdobeMobile資料庫至4.10.0
   * VHL資料庫至1.5.6
   * VHL-Nielsen資料庫至1.6.7

這個問題已藉由使用零高度檢視區在VPAID廣告播放時填滿舞台來解決。

* Zendesk #22110 - Analytics：新增:sc:心率追蹤呼叫的ssl欄位

SSL相關問題已修正，TVSDK中使用的VHL程式庫已更新至最新版本。

* Zendesk #22608 — 影片間歇性地顯示黑色熒幕(需要Flash Player22.0.0.175或更新版本)

在適用性位元速率期間，如果設定了最大位元速率限制，即使使用者端看到位置更新，且使用者端的行為就像在播放內容，重新載入視訊時斷時續會顯示黑色畫面。

**版本1.4.23** (809)

* Zendesk #2887 — 將廣告規則邏輯套用至TVSDK時的後置廣告略過問題

**注意**：此問題需要Flash播放器21.0.0.240或更新版本。

已修正將廣告規則邏輯套用至TVSDK時略過後置廣告的問題。

* Zendesk #19863 — 已捨棄VPAID媒體檔案的廣告

如果大型內嵌廣告有多個媒體檔案，且第一個廣告為VPAID廣告，則不會為即時資料流播放內嵌廣告。 此問題已改為擷取其他媒體檔案來解決。

* Zendesk #21021 — 延遲繫結音訊，造成音訊區段重複

**注意**：此問題需要Flash播放器21.0.0.240或更新版本。

音訊重複問題已修正。

* Zendesk #21125 — 從即時/線性廣告插播提早返回

**注意**：此問題需要Flash播放器21.0.0.240或更新版本。

此版本支援在廣告插播播放至完成之前從廣告插播回訪。 透過自訂資訊清單標籤指出提早傳回。

* Zendesk # 21369延遲繫結音訊導致時間不一致

**注意**：此問題需要Flash播放器21.0.0.240或更新版本。

已修正的音訊重複問題也已修正此問題。

* Zendesk #21760， 20921 — 搜尋時解除音訊視訊同步。

**注意**：此問題需要Flash播放器21.0.0.240或更新版本。

音訊重複問題已修正。

* Zendesk #22024 — 執行TVSDK時發生錯誤

已修正參考播放器啟動時未播放任何資料流並擲回例外狀況的問題。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime執行階段錯誤，錯誤碼為3357

**注意**：此問題需要Flash播放器21.0.0.197或更新版本。

已修正呼叫storeVoucher()時正確初始化deviceID而發生的隨機3357錯誤。

* Zendesk #21334 — 第三方廣告請求的TVSDK廣告請求逾時值

在此版本中，已新增全域廣告請求逾時。

**1.4.21版** (782)

* Zendesk #19580 TVSDK會等待內容解析程式完成後再傳送 `PTTimedMetadataChangedNotification` 通知

**注意**：此問題需要Flash播放器21.0.0.182或更新版本。

透過提供設定廣告標籤並新增自訂機會產生器的功能，顯示如何訂閱自訂提示以及如何在VOD檔案中處理這些提示，案頭參考播放器已解決此問題。

* Zendesk #20806 DVR視窗中的未來中段廣告在交換露營後不會觸發

**注意**：此問題需要Flash播放器21.0.0.182或更新版本。

此問題已透過更新應用程式以設定_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL， &quot;false&quot;)來解決，以停用PIP交換中的前段廣告插入，因此不會產生任何前段機會。

已引入排序功能來修正造成主要內容持續時間為負數的順序錯亂的廣告投放位置。

* Zendesk #20522：無法略過VPAID 2.0廣告

**注意**：此問題需要Flash播放器21.0.0.182或更新版本。

* 在廣告寬恕期間略過VPAID廣告，即可解決此問題。
* 當廣告插播原則設為略過時，仍會傳送廣告和廣告插播事件。 播放器狀態不一致。

此問題已解決，在略過廣告插播時行為正確且不會傳送事件。

* Zendesk #20955透過機會產生器在customParameters屬性中設定索引鍵值配對

**注意**：此問題需要Flash播放器21.0.0.182或更新版本。

為廣告請求建立廣告單位時，Auditude請求會剖析自訂引數的AuditudeSettings 。

此行為已變更，以便將來自Opportunity物件的自訂引數納入請求中。 此外，多個具有不同自訂引數的商機無法封裝在一個Auditude請求中。

* Zendesk #21227 - m3u8無法一致播放

**注意**：此問題需要Flash播放器21.0.0.211或更新版本。

此問題已透過允許TVSDK忽略資訊清單（HLS子設定檔）來解決，該資訊清單包含TVSDK不支援的AC3轉碼器（環繞）。

**1.4.20版** (762)

* Zendesk #19181 — 快速前進到即時點鎖定資料流。

**注意**：此問題需要Flash播放器20.0.0.306或更新版本。

* Zendesk #19286 — 在FER資料流中來回搜尋時發生Flash Player當機。

**注意**：此問題需要Flash播放器20.0.0.306或更新版本。

如果查詢需要太長的時間才能取得回應或通訊端正在關閉，則在Google Chrome中搜尋時偶爾發生的暫止問題可透過關閉查詢來解決。

* Zendesk #19305 — 播放具有A/V不連續性的資料流時遇到斷斷續續的播放問題。

**注意**：此問題需要Flash播放器20.0.0.306或更新版本。

此問題已藉由回報警告而解決。

* Zendesk # 19359 — 由於#EXT-X-FAXS-CM：屬性在設定層級資訊清單中的位置，Flash Player當機。

當標籤出現在播放清單中#EXT-X-FAXS-CM個別位元速率或區段之前的頂端播放清單時，此問題已解決。

* Zendesk #19489 - Fast Forward to Live Point外掛程式（即時資料流）

此問題與Zendesk #19181相同。

* Zendesk #19699 - TVSDK無法在WebVTT字幕曲目之間切換

此問題已解決，方法是在追蹤變更時進行播放器傾印並重新載入資訊清單，以及修正影響雙位元組WebVTT插圖示題追蹤名稱的UTF8字串轉換問題。

**版本1.4.19** (1.4.19.738)

* Zendesk #18234 — 使用CC中的Unicode字串播放Streams的Flash Player當機

此問題需要Flash PlayerFP 20.0.0.267或更新版本，並透過正確處理Unicode字串來解決。

* Zendesk #18304 - VPAID廣告的串流完整性支援

此功能需使用Flash PlayerFP 20.0.0.267或更新版本，已在1.4.19版中引入。

* Zendesk #18766 — 參考播放器無法在CC曲目名稱中顯示非拉丁Unicode字元

此功能需要Flash PlayerFP 20.0.0.267或更新版本，並已透過正確處理Unicode字串加以修正。

* Zendesk #18804 - Firefox 42中的播放器當機

此問題需要Flash PlayerFP 20.0.0.235或更新版本，與Zendesk #18723的問題相同。

* Zendesk #18864 -Flash Player完整外掛程式當機

此問題需要Flash PlayerFP 20.0.0.235或更高版本，並且與Zendesk #18723相同。

* Zendesk #18998 — 如果音訊和視訊時間戳記不相符，就會發生大量中斷的區段下載。

此問題已透過忽略時間戳記之間的間隙並僅播放下載內容來解決。

* Zendesk #19093 — 只能觀看一次具有即時和完整事件重播(FER)內容的中段廣告，但在快速轉送或搜尋經過廣告時無法再次觀看這些廣告

在Primetime的預設adPolicy選取器中，如果觀看了中段廣告，當您完成搜尋時，adBreak不會移至搜尋位置。 若要再次播放廣告，在搜尋之後，應用程式必須覆寫selectAdBreaksToPlay()函式。

* Zendesk #19101 — 倒退到無法解析的Midroll廣告會移除廣告位置。

此問題已透過允許播放器更新playbackMetrics時間、minimumOpportunityTime和時間表來解決。

* Zendesk #19102 - FER和秘訣模式問題

此問題需要Flash PlayerFP 20.0.0.267或更新版本，並透過正確設定advertisingMetadata.adSignalingMode來解決。

* Zendesk #19175 — 有時，前段廣告不會在首次播放資料流時顯示。

此問題已透過新API adRequestTimeout新增至AuditudeSettings以解決廣告要求逾時。 使用者現在可以覆寫預設的10s廣告請求逾時。

**版本1.4.18** (1.4.18.722)

* Zendesk #3324 - VMAP中沒有廣告媒體時，Primetime廣告報告不會追蹤廣告插播。

當廣告插播為空白時，系統未偵測到廣告插播開始和完成追蹤事件。 此問題已透過在空白廣告插播（例如VMAP AdBreak）上使用有效的AdSource節點傳送廣告插播開始Ping來解決。

**版本1.4.17** (1.4.17.702)

* Zendesk #17168 — 切換可見度後，字幕不會出現10秒左右

此問題已藉由為vtt標題檔案提供EXT-X-MEDIA-TIME標籤支援而解決。

* Zendesk #17983 — 如果無法為資訊清單下載任何金鑰，會導致整個資訊清單播放失敗

**注意**：您必須至少Flash PlayerFP 19.0.0.245或更高版本。

有時播放即時內容時，資訊清單中可能有無效的索引鍵（例如中斷期間），但其他時間範圍可能有有效的索引鍵，仍可播放。 先前，當無法下載資訊清單中列出的索引鍵時，整個資訊清單會失敗。 現在，資訊清單只有在無法下載所有列出的索引鍵時才會失敗。 如果部分金鑰有效，但部分金鑰無法下載，則會播放內容。 如果我們嘗試播放的區段需要我們未擁有的金鑰，還是會失敗。

* Zendesk #18554 — 串流完整性在某些情況下，會減少Cookie

**注意**：您必須至少Flash PlayerFP 19.0.0.245或更高版本。

已修正可能截斷Cookie值的Cookie操作程式碼錯誤。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 — 在Chrome中為串流完整性新增代理支援(需要Flash PlayerFP 19.0.0.207或更高版本)

這是增強功能。

* Zendesk #4244 - PTS變換影像時的串流問題

此問題已透過偵測滑鼠指向效果並管理每個裝載型別的不連續性來解決，而不具有一般性。

* Zendesk #4487 — 追蹤線性內容頻道

線上性資料流播放工作階段中，重新初始化視訊心率追蹤器即可解決此問題。

* Zendesk #17427 - Chrome (Win7)上的Proxy無法使用Adobe資料流完整性()

**注意**：解析度需要Flash PlayerFP 19.0.0.207或更高版本。

此問題與Zendesk #3732相同。

* Zendesk #17907 - pHLS Live Stream上的延遲，Flash Player為19

**注意**：解析度需要Flash PlayerFP 19.0.0.207或更高版本。

此問題已透過處理即時資料流解決，在重新載入即時資訊清單時，TS檔案的網域會變更，且檔案下載了兩次。

* Zendesk #17931 — 開頭為石板的HLS內容無法播放

**注意**：解析度需要Flash PlayerFP 19.0.0.207或更高版本。

此問題已藉由在第一個TS檔案的前2秒內處理沒有音訊的資料流而解決。

* Zendesk #17934 — 即時串流失敗，Flash為19.0.0.185

**注意**：解析度需要Flash PlayerFP 19.0.0.207或更高版本。

透過在區段邊界上處理音訊和視訊影格之間具有時間交錯的即時資料流，此問題已解決。

* Zendesk #17973 — 中段期間最新Flash Player19.0.0.185當機

**注意**：解析度需要Flash PlayerFP 19.0.0.207或更高版本。

透過處理具有中段廣告插入的未設為靜音的音訊，此問題已解決。 （剖析器開關會發生，並且在播放的任何時候，內容會轉換為中段廣告、或是在廣告播放中等等。）

* Zendesk #18049 — 使用Firefox 42 Beta進行Flash19當機

此問題與Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* Zendesk #4377：因廣告原則而略過廣告插播時，引發AD_BREAK_SKIPPED事件。

修正方法是在略過廣告時新增AD_BREAK_SKIPPED。

* Zendesk #4496 — 資料流完整性：重新導向代碼化資料流時發102100錯誤。

修正是新增支援透過TVSDK設定AVNetworkConfiguration屬性useCookieHeaderForAllRequests。

* Zendesk #17179 — 加密內容的多個SAP變更導致Flash播放器當機。

部分加密內容錄放期間的當機問題已修正。

**注意**：此修正需要Flash Player19.0.0.200或更新版本。

* Zendesk #17499 — 我們如何在觀看後移除midroll，但從選件內容移除前置滾動

已新增型別至AdBreakTimelineItem (AdBreakTimelineItem.placementType)，讓AdPolicySelector可針對前段、中段和後段內容傳回不同原則。

* Zendesk #17665 — 頻寬節流

此修正是移除邏輯，以便在緩衝開始時將目標緩衝區大小變更為初始緩衝區大小。

**1.14.14版** (1.4.14.771)

* Zendesk #17363 — 修正參考播放器的README檔案

   * 釐清下載和安裝playerglobal.swc的說明。
   * 新增使用特定flash player版本更新專案組態的指示。
   * 更新AdvertisingOverlay專案設定以使用最低播放器版本。
   * 更新ReferenceCore專案設定以使用特定播放器11.9版

* Zendesk #17471 — 播放器凍結

部分修正搜尋後廣告沒有從頭開始播放的問題。

* Zendesk #17496 — 在DVR視窗中搜尋返回時，未解析Podbuster

提供每個廣告插播的自訂引數。

**版本1.4.13** (1.4.13.660)

* Zendesk #4037 — 無可用的設定檔錯誤(需要Flash Player18.0.0.232或更高版本)

修正查詢引數包含「http」時的url剖析問題

* Zendesk #4260 - IE11中的Flash Player18當機(需要Flash Player18.0.0.232或更新版本)

修正使用IE11以全熒幕模式播放視訊時的當機問題

* Zendesk #4262 - Adobe Primetime播放器在windows 10上當機(需要Flash Player18.0.0.232或更高版本)

修正在Windows上使用FireFox以全熒幕模式播放視訊時的當機問題。

* Zendesk #4279 - iOS和案頭上的HLS TVSDK廣告插入–302重新導向問題

修正URL沒有副檔名，無法正確辨識其型別的問題

* Zendesk #4306 — 僅在Win上全熒幕時發生Flash Player當機(需要Flash Player18.0.0.232或更高版本)

修正在Windows上以全熒幕模式播放視訊時的當機問題。

* Zendesk #4480 — 遺失ID3標籤事件(需要Flash Player18.0.0.232或更新版本)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增強：處理特定媒體檔案URL中的動態元素。

更新Creative重新封裝服務，以正確處理具有動態創意URL的廣告。

* ptplay - 2114 - MP4播放支援。

現在支援MP4內容的基本播放，包括播放、暫停和搜尋。

下列專案需要Flash Player18.0.0.225或更高版本：

* Zendesk #3992 — 其他TrickPlay速度。

TrickPlay現在接受高於16x的速率：+/- 32、+/-64和+/-128。

* Zendesk #3113 -Flash Player外掛程式當機

修正嘗試在Mac Firefox上播放重新導向廣告時的當機問題。

* Zendesk #4037 — 沒有可用的設定檔錯誤
* Zendesk #4262 - Adobe Primetime播放器在windows 10上當機

修正全熒幕播放期間在Windows Firefox中當機的問題。

**1.4.11版** (1.4.11.648)

* Zendesk #1869 — 變更字型大小的問題(需要Flash Player18.0.0.200)

允許在WebVTT註解程式碼中使用註解大小。

* Zendesk #3113 -Flash Player外掛程式當機(需要Flash Player18.0.0.200)
* Zendesk #3268 — 桌上型：視訊播放器在+- 40/50秒後開始閃爍，並在+- 90秒後開始變黑(需要Flash Player18.0.0.200)

修正中繼視訊錯誤。

* Zendesk #3670 — 在參考播放器中搜尋時，VOD中出現INVALID_PARAMETER錯誤(需要Flash Player18.0.0.200)

偵測到新期間時，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 — 在Chrome上將串流完整性設定為「開啟」的Flash Player當機(需要Flash Player18.0.0.200)

修正Pepper原生網路模式中的當機

* Zendesk #3905 — 在CDN上代管時，TVSDK播放器未載入

修正pageDomain與swf網域不同時尋找萬用字元權杖的問題。

**1.4.10版** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player在Firefox上讓Flash當機

修正Mac上Firefox偶爾的Flash Player當機，在外部熒幕上播放的資料流會切換至較高的位元速率資料流。(需要Flash Player18.0.0.160)

* Zendesk #3268 — 桌上型電腦：影片播放器在 `+-` 40/50秒後開始變黑 `+-` 90秒

修正Mac Chrome上串流開始忽隱忽現，最終變成黑色的問題。 (需要Flash Player18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填入巨集

   * 如果內嵌廣告具有不良創意，則會顯示錯誤碼400。
   * `[ERRORCODE]` 巨集將會進行URL編碼

* Zendesk #3601 — 增強功能要求：包裝函式隨附管理

   * TVSDK會顯示包含資源（html、iframe或靜態）的包裝函式隨附，以接近內嵌。 （如果內嵌不含該大小的字元）
   * 除非用於顯示，否則會忽略具有資源的包裝函式。 （不用於追蹤）
   * 只有不含資源的包裝函式夥伴才會用於追蹤目的。 （僅包含追蹤的包裝函式隨附）

**版本1.4.9**

* Zendesk #2615 — 從案頭顯示移除HLS檢視的問題

已將clearVideo()方法新增至MediaPlayer。 透過從StageVideo物件清除AVStream來清除顯示的視訊影格。 只有在視訊已暫停時才能呼叫，而且必須先呼叫replaceCurrentResource或replaceCurrentItem，才能再次呼叫play()。

* Zendesk #3169 — 透過Adobe Analytics整合更新參考播放器

參考播放器已更新並整合Adobe Analytics

* Zendesk #3296 — 桌上型HLS TVSDK — 未播放VAST第三方廣告

HLS格式的MIME型別區分大小寫，這不正確，已變更為不再區分大小寫

**版本1.4.8**

* Zendesk #2737 — 案頭播放器 — 錯誤106000 (需要Flash Player17.0.0.184)
* Zendesk #3007 — 更新為Flash Player17後未出現前段廣告(需要Flash Player17.0.0.184)
* Zendesk #3085 — 案頭HLS播放器在60秒後擲回106000錯誤(需要Flash Player17.0.0.184)

**版本1.4.7**

* Zendesk #2760 — 在TrickPlay模式期間忽略DISCONTINUITY標籤(需要Flash Player版本17.0.0.158)
* Zendesk #2760 — 在TrickPlay模式期間忽略DISCONTINUITY標籤(需要Flash Player版本17.0.0.158)

**版本1.4.6**

* Zendesk #2652 — 案頭HLS的Auditude檔案，釐清案頭HLS檔案的Auditudemedia_id

**版本1.4.5**

* Zendesk #2256 — 存取主要播放清單，更新PSDK以傳送主要播放清單上訂閱標籤的timedMetadata事件。 (需要Flash Player版本17.0.0.134)
* Zendesk #2417 — 播放器嘗試在播放開始前下載字幕，WebVTT使用錯誤的區段號碼變數進行區段號碼比對。 只有區段索引從零開始的媒體才會顯示錯誤。 (需要Flash Player版本17.0.0.134)
* Zendesk #2537 — 搭配Chrome使用Pepper外掛程式時，Flash播放器當機(需要Flash Player版本17.0.0.134)
* Zendesk #2547 — 阿拉伯字幕：文字應靠右對齊(需要Flash Player版本17.0.0.134)

**版本1.4.4**

* Zendesk #1561 — 回覆： `[Adobe Primetime]` 更新：HLS使用者端容錯移轉支援案頭PSDK中的PROGRAM-DATE-TIME (需要Flash Player版本16.0.0.305或更新版本)
* Zendesk #2197 - `[Ads]` 追蹤廣告錯誤
* Zendesk #2286 — 功能要求：提供廣告載入狀態的資訊(VPAID)
* Zendesk #2285 — 功能要求：在指定的逾時期間後略過廣告
* 錯誤#3921755 - Flash Player中的OpenSSL程式庫更新至1.0.1L版(需要Flash Player版本16.0.0.305或更新版本)

**版本1.4.2**

* Zendesk #1303 — 隱藏式字幕的垂直位移(需要Flash Player版本16.0.0.235或更新版本，預計發行日期：2014年12月)
* Zendesk #1870 — 開啟與關閉隱藏式字幕(需要Flash Player版本16.0.0.235或更新版本，預計發行日期： 2014年12月)
* Zendesk #2110 — 在VPAID廣告期間嘗試進入全熒幕後播放卡住(需要Flash Player版本16.0.0.235或更高版本，預計發行日期： 2014年12月)
* Zendesk #2199 - `[VPAID]` 搜尋過去的廣告插播時，播放器未回應
* Zendesk #2358 — 回覆： `[Analytics]` 不正確的章節資料

**版本1.4.1**

* 更新中斷API，以符合Android和iOS實作。

**1.4.0版**

* Zendesk #1024 — 透過資訊清單從資料流中移除廣告的功能
* Zendesk #1423 - HLS播放失敗正在鎖定Flash Player（未報告錯誤）
* Zendesk #1674 — 未顯示ClosedCaption，遺失0x03 ETX程式碼時顯示正確的708字幕。

## 已知問題 {#known-issues}

* 隱藏式字幕無法搭配純音訊內容使用，因為字幕系統需要視訊才能運作。
如果沒有視訊，就沒有檢視區尺寸，如果沒有檢視區尺寸，您將無法顯示註解的任何圖形。
* 由於Chrome沙箱限制，Google Chrome中的資料流完整性稍微變慢。
* 在TVSDK 1.4中，如果您停用自動播放，當播放器閒置至少一分鐘時，可能會發生DRM錯誤。 若要解決此問題，當您停用自動播放但預先載入資產時，請修改 `ReferenceCore.as` 透過變更以下專案的內容 `onPlaybackManagerPrepared`：

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **版本1.4.13** PTPLAY-8501 — 當VMAP傳回兩個直接MP4非轉碼廣告時，相同的後援廣告會播放兩次。

* **版本1.4.2** 在Flash Player版本16發行版本中，當播放器進入空白緩衝事件後，ABR的「關機」邏輯發現問題。 此問題會防止在播放器進入緩衝狀態後，位元速率在不良的頻寬環境中關閉。 若要解決此問題，請讓應用程式設定 `BufferControlParameters.initialBufferTime` 與相同 `BufferControlParameters.playbackBufferTime` 在緩衝狀態期間暫時(即在 `BufferEvent.BUFFERING_BEGIN` 事件)，然後將其重設為上的設定值 `BufferEvent.BUFFERING_END` 事件。 此問題的修正會在Flash Player版本16的下一個修補程式版本中提供。

* **1.4.0版**

   * PTPLAY-1634 — 相同的「已訂閱」標籤在不同的即時視窗中具有不同的時間戳記。 當即時視窗移動時，每個視窗中的相同標籤應該有相同的時間戳記。 但有時，相同的標籤會有不同的時間戳記。
   * PTPLAY-28 - MediaPlayer時間軸不包含空白分行符號。
   * 跨網域原則檔案(crossdomain.xml)需要從不同網域串流內容的許可權。 [設定用於HTTP串流的crossdomain.xml檔案](https://helpx.adobe.com/adobe-media-server/dev/configure-dynamic-streaming-live-streaming.html).
   * 錯誤#3694203 — 在DVR串流中，從播放中段搜尋另一個中段廣告提示可能會導致瀏覽器凍結
   * 錯誤#3753725 — 如果已觀看廣告插播，則未考慮selectPolicyForSeekIntoAd
   * 錯誤#3754529 — 在即時DVR資料流中搜尋時，不會從資料流中移除前段廣告
   * 錯誤#3761896 — 如果在廣告播放期間允許搜尋，則廣告標籤將在搜尋後重新調整。 因應措施是在搜尋期間不使用ITEM_UPDATED回呼
   * 錯誤#3779889 — 在Video Analytics中到達特技播放結尾時，不會進行完整呼叫
   * 錯誤#VA-779 — 未針對具有心率支援參考實作的增強視訊分析傳送位元速率變更事件心率 — 未在範例應用程式中實作特技播放。

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
