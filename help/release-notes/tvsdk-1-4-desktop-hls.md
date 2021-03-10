---
title: Desktop HLS的TVSDK 1.4發行說明
description: 案頭版HLS的TVSDK發行說明說明TVSDK DHLS中的新增或變更、已解決和已知問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5196'
ht-degree: 0%

---


# TVSDK 1.4 for Desktop HLS發行說明{#tvsdk-for-desktop-hls-release-notes}

案頭版HLS的TVSDK發行說明說明TVSDK DHLS中有哪些新增或變更、已解決和已知問題。

## 新功能{#new-features}

**1.4.31**

* **CRS廣告的多CDN支援**

   * 依預設，所有轉碼資產都將裝載在Akamai的Adobe擁有的CDN上。 在最新版本中，Adobe創意重新封裝服務(CRS)提供將轉碼創作元素上傳至客戶指定之多個CDN的功能。
   * 新增API至TVSDK，以啟用在未使用預設URL時指定最終的CRS創意URL。 請參閱檔案以瞭解如何使用這些新API。

### 舊版{#new-features-previous}的新功能

**1.4.30**

* **帳單量度**

為了迎合只想支付所用費用（而非固定費率，不論實際用途）的客戶，Adobe會收集使用量度，並使用這些度量來決定向客戶收取的費用。

**一點四點二四**

* **持久網路連接**

重要：您至少必須安裝AdobeFlash Player22版或更高版本。
持續網路連線會建立並儲存可重複用於多個請求的網路連線內部清單，而非為每個網路要求開啟新連線。 持續的網路連線應能提高效率並減少網路程式碼的延遲。

在這個版本中，Mac上的Apple Safari和Mozilla Firefox不支援此功能。

**一點四點一九**

* VPAID廣告的串流完整性支援。
* 已針對Firefox 42及更新版本，在Flash播放器FP 20.0.0.267中啟用靜音標籤選項，方法是修正擱置問題。

**一點四點一八**

* Primetime Desktop HLS TVSDK現在支援VPAID 2.0線性SWF創意素材，以提供豐富的互動串流內廣告體驗。

**1.4.10**

* **廣告備援、廣告選擇邏輯中的菊花鏈(Zendesk #3103)** 對於啟用備援規則的VAST廣告（創意人員）,TVSDK會將具有無效MIME類型的廣告視為空廣告，並嘗試在其位置使用備援廣告。您可以設定備援行為的某些方面。

如需詳細資訊，請參閱[VAST和VMAP廣告的廣告後援](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)。

**1.4.8**

* **視訊心率程式庫(VHL)已更新至1.5版**

   * 能夠以視訊開始和／或視訊／廣告／章節開始傳送中繼資料作為內容資料
   * 網路流量減少——心率平均會減少，而且會變小。

**1.4.7**

* **現場個人化支援**

支援Adobe個性化伺服器的現場安裝，以定制客戶端的個性化請求，以轉到不同的端點。

**1.4.6**

* **範例AES加密(需要Flash Player版本17.0.0.134)**

現在支援範例型AES加密。

**1.4.2**

* **視訊心率程式庫(VHL)更新至1.4.0.1版**

   * 新增搭配Adobe Analytics視訊基本工具，搭售其他SDK或播放器的不同分析使用案例的能力。
   * 已移除trackAdBreakStart和trackAdBreakComplete方法來最佳化廣告追蹤。 廣告插播是從trackAdStart和trackAdComplete方法呼叫推斷而得。
   * 追蹤廣告時不再需要播放頭屬性。

**1.4.0**

* **使用替代內容** 取代封鎖訊號在1.4 TVSDK更新中，TVSDK現在也支援針對線性內容進行區域封鎖並返回。TVSDK現在可以並行處理主要和替代的兩個資訊清單檔案，以便監控封鎖訊號，即使替代原始程式設計顯示替代程式設計。

* **移除／取代C3** AdsNow，您不需要額外的準備工作，就能將新廣告動態插入從C3視訊視訊(VOD)資產。TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 此強大的新功能在廣播期間播放即時／線性內容時也很有用，而且會立即下拉以做為隨選內容，而無需適當的時間來「清理」資產。

## 已解決問題{#resolved-issues}

>[!NOTE]
>
>強烈建議所有使用CRS的TVSDK客戶升級至iOS、Android和Desktop HLS上的至少TVSDK 1.4.32。 此升級將取代現有應用程式實作的下載。 升級後，請在Proxy工具（例如Charles）中檢查CRS創意URL要求，以確認路徑中的版本是否反映3.1版。例如，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**1.4.41版**

* Zendesk #33777 - DHLS散發組建版本的Localhost Token SWF已過期。

   在DHLS上更新PMP展示的localhost Token。

### 已解決舊版{#resolved-issues-previous}中的問題

**1.4.38** (891)版

* Zendesk #30731 - TVSDK不會在AdBreak中播放多個VPAID廣告。

   修正AdBreak中多個VPAID廣告的播放。

* Zendesk #29968 - Double Billboard。

   當發生ABR切換時，視訊播放器可重複時段的最後一段。 因此，有時會重複最後一段預播。 這個問題已經修正。

**1.4.35** (879)版

* Zendesk #26058 —— 支援原生VPAID事件

**1.4.33** (873)版

* Zendesk #21701 —— 傳送1401 CRS要求的原始創意URL，而非標準化URL。

   已修正依據CRS後端的要求，要求重新封裝的URL進行轉碼的問題。
* Zendesk #26197 —— 變形壓縮未在所需的顯示解析度中播放。

   **注意**:此問題需要Flash播放器24.0.0.194或更新版本。

   使用長寬比表中缺失條目來計算輸出寬度的問題已經修正。

* Zendesk #26840 —— 第二次嘗試後IE11 + Windows7上的HDCP檢測失敗。

   **注意**:此問題需要Flash播放器24.0.0.218或更新版本。

   此問題已解決，方法是修改AdobeCP的主訊息佇列處理，以重複整個佇列，而不是僅封鎖第一條訊息。

* Zendesk #27460 —— 新的Akamai帳戶無法處理POSTCDN請求。

   新的CDN帳戶無法處理POSTCDN請求。 此問題已解決，方法是更新程式碼，使cdn.auditude.com廣告請求成為GET，而非POST。
* Zendesk #27619 - Windows 10Flash崩潰

   **注意**:此問題需要Flash播放器24.0.0.218或更新版本。

   此問題已透過防止長URL造成錯誤而解決。

* Zendesk #28218 —— 追蹤事件不會在從繼續點進行回傳時觸發

   此問題與Zendesk #26592中的問題相同。 當媒體播放器處於VOD串流的PREPARED狀態時，允許搜尋操作的問題已經修正。

**版本1.4.32** (867)

* Zendesk #26592當從繼續點開始播放時，不會觸發追蹤事件

當繼續點不為零時，程式碼不會更新前段廣告插播項目。 此問題已解決，方法是新增邏輯，在範圍開始時間不符時重新整理程式碼。

* 第二次播放資產時，不會播放Zendesk #27022廣告

陣列方法的例外情況已經修正。

**1.4.30版** (855)

TVSDK在此版本中已解決下列問題：

* Zendesk #22898 —— 字幕缺失不應導致播放失敗。

**注意**:此問題需要Flash播放器23.0.0.185或更新版本。

此問題已解決，因為允許TVSDK繼續播放，即使資訊清單遺失WebVTT M3U8，而且只要註冊警告即可。

* Zendesk #23454 —— 第三方廣告(VPAID)未正確處理

此問題已透過根據內容ID（而非時間範圍）正確處理VPAID廣告來解決。

* Zendesk #24528 —— 帳單的TVSDK使用量度。

重要：此問題需要Flash播放器23.0.0.185或更新版本。

* Zendesk # 25432調整播放器大小期間隱藏字幕問題。

重要：此問題需要Flash播放器23.0.0.185或更新版本。

字幕顯示紋理地圖程式碼已修正，可在調整播放器大小期間正確處理座標。

視訊心率程式庫(VHL)已更新至1.5.9版，以解決下列問題：

* Zendesk #23730 —— 位元速率量度為空

此問題已透過追蹤VideoAnalyticsTracker中的位元速率變更來解決。

* 新增API assetDuration至PTVideoAnalyticsTrackingMetadata，以更新即時／線性串流的資產持續時間。

**1.4.28版** (848)

* Zendesk #25027 - Auditude在1.4.27案頭版本中無法運作

此問題已解決，方法是新增程式碼以檢查AUDITUDE_METADATA_KEY，並讓AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互換。

* Zendesk #24428 —— 使用TVSDK播放DRM HLS時經常發生的緩衝問題

此問題已解決，因為當沒有廣告設定時，TVSDK可以透過消除時間軸上的前段廣告保留和即時保留保留保留來加速處理。

* Zendesk #24344 —— 禁用WebVTT檔案以改進啟動時間。

**注意**:此問題需要Flash播放器23或更新版本。

此問題已解決，只有在需要顯示標題時，才會載入WebVTT檔案。

* Zendesk #24994 —— 從商務休息返回時，隱藏字幕從播放器上刪除

**注意**:此問題需要Flash播放器23或更新版本。

偽EOC代碼導致標題顯示消失。 此問題已解決，強制608字幕代碼RU2、RU3和RU4在目前的作用中視窗中提供正確的可見度。

**1.4.27版** (844)

* Zendesk #21554 —— 未針對應用程式類型= video/mp4引發TVSDK錯誤信標

此問題已解決，方法是啟用TVSDK ping無效資產格式上的正確錯誤追蹤URL。

* Zendesk #23402 —— 不完整的廣告播放

**注意**:此問題需要Flash播放器23或更新版本。

在某些要求發生404錯誤後，可能會發生當機。 此問題已解決，方法是確保在處理響應時不關閉連接。 此解析度可確保VPAID廣告檔案不會被錯誤計算，因此在下載時不會發佈。

* Zendesk #23621 - 400和404上的重試失敗

**注意**:此問題需要Flash播放器23或更新版本。

修正在不同描述檔之間切換時，造成DRM中繼資料損毀的問題。

* Zendesk #23705 - AdSinct中斷期間凍結視訊廣告

**注意**:此問題需要Flash播放器23或更新版本。

此問題與Zendesk #23621中的問題相同。

* Zendesk #23905 —— 廣告插播時有些廣告插播跳過

**注意**:此問題需要Flash播放器23或更新版本。

已修正Windows原生網路程式碼，以確保連線不會關閉其他連線目前使用的控點。

* 票證#24029 - HLS FER串流不會在中間卷。json檔案中播放所有中間卷廣告。

通過允許客戶在Opportunity實例上單獨設定自定義參數，以便客戶不必覆蓋OpportunityGenerator，此問題得到瞭解決。

**版本1.4.26** (839)

* Zendesk #18854 —— 根據CRS規則更新創意選擇邏輯
   * 提供支援以根據CRS規則更新創意選擇邏輯

* Zendesk #22725 —— 在案頭應用程式範例中的playbackManager.beginPlayback()實作

   * 修正方法：移除startPlaybackFromFlashVars結尾處的此重複呼叫，作為從setupVideo()呼叫的方法

* Zendesk #22807 - SeekManager空參考例外

   * 通過在SeekManager中提供與_dispatcher相關的必要NULL指針保護來修正

* Zendesk #22822 —— 使用TVSDK播放清楚的HLS時經常進行緩衝

   * 修正方法：移除adSignalingModeOpportunityGenerator（如果沒有廣告）產生的初始機會

* Zendesk #23378 —— 串流完整性區塊rules.xml

   * 透過串流完整性工作流程載入rules.xml檔案來修正

**1.4.24** (817)版

* Zendesk #19851 —— 當播放器適應不同的位元速率時，它會在新位元速率上跳回數個畫格，讓體驗變得尷尬

**注意**:此問題需要Flash播放器22.0.0.175或更新版本。

DRM適配器在下載一小部分段後重置無法正確恢復的問題已經解決。

* Zendesk #20784 - Analytics:觸發內容完成即時視訊轉場

此問題已解決，方法是新增API(trackVideoComplete)，以手動觸發LINEAR/LIVE視訊追蹤工作階段中的內容完成。

已更新下列程式庫：

* Zendesk #21643 - VPAID廣告無法完整播放

   * AdobeMobile程式庫至4.10.0
   * VHL程式庫至1.5.6
   * VHL-Nielsen資料庫至1.6.7

當VPAID廣告播放時，使用零高度檢視埠來填滿舞台，以解決此問題。

* Zendesk #22110 - Analytics:新增h:sc:ssl欄位至心率追蹤呼叫

已修正SSL相關問題，而TVSDK中使用的VHL程式庫已更新為最新版本。

* Zendesk #22608 —— 視訊間歇性顯示黑幕(需要22.0.0.175或更新版本的Flash Player)

在可調式位元速率期間，在位元速率上限下，即使用戶端看到位置更新，視訊的重新載入仍會間歇性地顯示黑幕，而用戶端的動作就像在播放內容一樣。

**1.4.23版** (809)

* Zendesk #2887 —— 將廣告規則邏輯套用至TVSDK時的滾動廣告跳過問題

**注意**:此問題需要Flash播放器21.0.0.240或更新版本。

已修正將廣告規則邏輯套用至TVSDK時，會略過前段廣告的問題。

* Zendesk #19863 —— 放棄VPAID媒體檔案的廣告

如果大型內嵌廣告包含多個媒體檔案，而VPAID廣告是第一個廣告，則內嵌廣告不會針對即時串流播放。 此問題已透過取用不同的媒體檔案來解決。

* Zendesk #21021 —— 延遲裝訂音訊導致音訊區段重複

**注意**:此問題需要Flash播放器21.0.0.240或更新版本。

音訊重複問題已修正。

* Zendesk #21125 —— 提早從即時／線性廣告放假返回

**注意**:此問題需要Flash播放器21.0.0.240或更新版本。

此版本支援在播放廣告片段至完成之前，從廣告片段返回。 透過自訂資訊清單標籤指出提早傳回。

* Zendesk # 21369延遲綁定音頻導致時間不一致

**注意**:此問題需要Flash播放器21.0.0.240或更新版本。

已修正的音訊重複問題也已修正此問題。

* Zendesk #21760, 20921 - Audio Video Desync on Seek。

**注意**:此問題需要Flash播放器21.0.0.240或更新版本。

音訊重複問題已修正。

* Zendesk #22024 —— 執行TVSDK時發生錯誤

參考播放器未播放任何串流，且在啟動時拋出例外的問題已經修正。

**版本1.4.22** (791)

* Zendesk #17580 - Primetime執行時期錯誤，代碼為3357

**注意**:此問題需要Flash播放器21.0.0.197或更新版本。

已修正呼叫storeVoucher()時，正確初始化deviceID而發生的隨機3357錯誤。

* Zendesk #21334 - TVSDK廣告要求第三方廣告要求逾時值

在此發行中，已新增全域廣告請求逾時。

**1.4.21版** (782)

* Zendesk #19580 TVSDK等待內容解析器完成後再傳送`PTTimedMetadataChangedNotification`通知

**注意**:此問題需要Flash播放器21.0.0.182或更新版本。

此問題已在Desktop Reference Player中解決，因為它提供設定廣告標籤的功能，並新增自訂機會產生器，顯示如何訂閱自訂提示，以及如何在VOD檔案中處理這些提示。

* Zendesk #20806在交換攝影機後，DVR視窗中的未來中轉廣告不會觸發

**注意**:此問題需要Flash播放器21.0.0.182或更新版本。

此問題已解決，方法是將應用程式更新為設定_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;)，以停用PIP交換中的前段廣告插入，因此不會產生前段廣告插入機會。

已引入排序功能，以修正導致主要內容持續時間不佳的亂序廣告位置。

* Zendesk #20522:無法略過VPAID 2.0廣告

**注意**:此問題需要Flash播放器21.0.0.182或更新版本。

* 此問題已透過在廣告容錯期間略過VPAID廣告而解決。
* 當adbreak原則設為略過時，廣告和廣告分段事件仍會傳送。 播放器狀態不一致。

此問題已解決，以在跳過廣告中斷時正常運作，而非分派事件。

* Zendesk #20955通過opportunity生成器在customParameters屬性中設定鍵值對

**注意**:此問題需要Flash播放器21.0.0.182或更新版本。

當建立廣告請求的廣告單位時，Auditude請求會剖析AuditudeSettings的自訂參數。

此行為已更改為在請求中包含來自Opportunity對象的自定義參數。 此外，不同自訂參數的多個機會無法整合在單一Auditude要求中。

* Zendesk #21227 - m3u8無法一致地播放

**注意**:此問題需要Flash播放器21.0.0.211或更新版本。

此問題已解決，因為允許TVSDK忽略包含TVSDK不支援（環繞）的AC3轉碼器的資訊清單（HLS子設定檔）。

**1.4.20版** (762)

* Zendesk #19181 - Trick play fast forward to live point locks up stream.

**注意**:此問題需要Flash播放器20.0.0.306或更新版本。

* Zendesk #19286 —— 在FER流中來回搜索時發生Flash Player崩潰。

**注意**:此問題需要Flash播放器20.0.0.306或更新版本。

在Google Chrome中搜尋時偶爾發生的掛起問題已透過關閉查詢來解決，如果查詢需要太長時間才能收到回應，或通訊端已關閉。

* Zendesk #19305 —— 播放A/V不連續的串流時，遇到不順暢的播放。

**注意**:此問題需要Flash播放器20.0.0.306或更新版本。

此問題已透過報告警告而解決。

* Zendesk # 19359 -Flash Player因#EXT-X-FAXS-CM的位置而崩潰：屬性。

當#EXT-X-FAXS-CM標籤出現在播放清單中個別位元速率或區段之前的頂端播放清單時，此問題已解決。

* Zendesk #19489 - Fast Forward to Live Point stols plugin（即時串流）

此問題與Zendesk #19181相同。

* Zendesk #19699 - TVSDK無法在WebVTT子標題軌道之間切換

此問題已解決：在追蹤變更時，讓播放器轉儲並重新載入資訊清單，並修正影響雙位元組WebVTT標題追蹤名稱的UTF8字串轉換問題。

**1.4.19版** (1.4.19.738)

* Zendesk #18234 - CC中使用Unicode字串播放串流的Flash Player當機

此問題需要Flash PlayerFP 20.0.0.267或更新版本，並且已透過正確處理Unicode字串來解決。

* Zendesk #18304 - VPAID廣告的串流完整性支援

此功能需要FP 20.0.0.267或更新版本的Flash Player，並已在1.4.19版中推出。

* Zendesk #18766 - Reference Player無法在CC音軌名稱中顯示非拉丁文Unicode字元

此功能需要FP 20.0.0.267或更新版本的Flash Player，並且已修正為正確處理Unicode字串。

* Zendesk #18804 - Firefox 42中的播放器當機

此問題需要FP 20.0.0.235或更新版本Flash Player，與Zendesk #18723相同。

* Zendesk #18864 -Flash Player完整增效模組當機

此問題需要FP 20.0.0.235或更高版本的Flash Player，與Zendesk #18723相同。

* Zendesk #18998 —— 如果音訊和視訊時間戳記不符，就會發生不連續的區段下載。

此問題已透過忽略時間戳記之間的間隔，並只播放已下載的內容而解決。

* Zendesk #19093 —— 只能使用即時和全事件重播(FER)內容觀看一次中轉廣告，但是當快速轉送或透過廣告搜尋時，無法再觀看這些廣告

在Primetime的預設adPolicy選擇器中，如果觀看中段廣告，在您完成搜尋時，adBreak不會移至搜尋位置。 若要再次播放廣告，在搜尋後，應用程式需要覆寫selectAdBreaksToPlay()函式。

* Zendesk #19101 —— 將廣告重新捲入未解決的Midroll廣告中，將刪除廣告位置。

此問題已解決，可讓播放器更新playbackMetrics時間、minimumOpportunityTime和時間軸。

* Zendesk #19102 - FER和秘訣模式問題

此問題需要Flash PlayerFP 20.0.0.267或更新版本，並且已透過正確設定advertisingMetadata.adSignalingMode來解決。

* Zendesk #19175 —— 有時，首播廣告不會在第一次播放串流時顯示。

此問題已解決，方法是將新的API adRequestTimeout新增至AuditudeSettings，以取得廣告請求逾時。 使用者現在可以覆寫預設的10秒廣告請求逾時。

**1.4.18版** (1.4.18.722)

* Zendesk #3324 - Primetime廣告報告不會在VMAP中沒有廣告媒體時追蹤廣告插播。

當廣告插播是空的時，廣告插播開始和完成追蹤事件都未被Ping通。 此問題已解決，方法是在空廣告插播（例如VMAP AdBreak）上傳送廣告插播開始ping，並提供有效的AdSource點頭。

**1.4.17版** (1.4.17.702)

* Zendesk #17168 —— 切換可見度後，字幕不會顯示10秒左右

此問題已解決，因為它支援EXT-X-MEDIA-TIME標籤（vtt標題檔案）。

* Zendesk #17983 —— 無法下載資訊清單的任何鍵，導致整個資訊清單播放失敗

**注意**:您至少必須有Flash PlayerFP 19.0.0.245或更高版本。

有時播放即時內容時，資訊清單中可能會有無效的索引鍵（例如，封鎖期），但其他時間範圍可能有有效的索引鍵，而且仍會播放。 以前，當資訊清單中列出的索引鍵無法下載時，整個資訊清單會失敗。 現在，資訊清單只會在無法下載所有列出的索引鍵時失敗。 如果某些鍵有效，但無法下載其中某些鍵，則內容將會播放。 如果我們嘗試播放需要沒有索引鍵的區段，我們仍會失敗。

* Zendesk #18554 - Stream Integrity修剪Cookies（在某些情況下）

**注意**:您至少必須有Flash PlayerFP 19.0.0.245或更高版本。

Cookie操作程式碼中可能會截斷Cookie值的錯誤已修正。

**版本1.4.16** (1.4.16.684)

* Zendesk #3732 —— 新增Chrome中Proxy的串流完整性支援(需要Flash PlayerFP 19.0.0.207或更高版本)

這是增強功能。

* Zendesk #4244 - PTS變換時的串流問題

此問題是透過偵測滑鼠指向效應並管理每個負載類型的不連續性而解決的。

* Zendesk #4487 —— 追蹤線性內容頻道

此問題已解決，方法是線上性串流播放工作階段期間重新初始化視訊心率追蹤器。

* Zendesk #17427 -Adobe串流完整性無法透過Chrome上的代理運作(Win7)()

**注意**:該決議要求Flash PlayerFP 19.0.0.207或更高版本。

此問題與Zendesk #3732相同。

* Zendesk #17907 - pHLS Live Stream的延遲與Flash Player19

**注意**:該決議要求Flash PlayerFP 19.0.0.207或更高版本。

此問題已解決，方法是處理在重新載入即時資訊清單時，TS檔案的網域會變更的即時串流，而且檔案已下載兩次。

* Zendesk #17931 —— 開始時帶石板的HLS內容無法回放

**注意**:該決議要求Flash PlayerFP 19.0.0.207或更高版本。

此問題已解決，方法是在第一個TS檔案的前2秒處理沒有音頻的流。

* Zendesk #17934 —— 帶19.0.0.185Flash的即時串流故障

**注意**:該決議要求Flash PlayerFP 19.0.0.207或更高版本。

此問題已解決，方法是在處理即時串流時，在區段邊界的音訊和視訊影格之間進行時間交錯。

* Zendesk #17973 —— 最新Flash Player19.0.0.185在中端時崩潰

**注意**:該決議要求Flash PlayerFP 19.0.0.207或更高版本。

此問題已透過使用中段廣告插入來處理未混音音訊而解決。 （解析器切換會發生，且在播放中的任何點，內容會轉換至中間廣告，或在廣告播放中間，依此類推。）

* Zendesk #18049 —— 使用Firefox 42 beta版Flash19當機

此問題與Zendesk #17973相同。

**版本1.4.15** (1.4.15.678)

* Zendesk #4377:因為廣告原則，在跳過廣告插播時觸發AD_BREAK_KRIPPED事件。

修正是在跳過廣告時新增AD_BREAK_BRIKPED。

* Zendesk #4496 —— 流完整性：錯誤102100，其重新導向至Token化串流。

修正方法是透過TVSDK新增AVNetworkConfiguration屬性useCookieHeaderForAllRequests的設定支援。

* Zendesk #17179 -Flash播放器在加密內容的多個SAP變更上當機。

已修正播放某些加密內容時的當機問題。

**注意**:此修正需要19.0.0.200Flash Player或更高版本。

* Zendesk #17499 —— 如何不在觀看後移除midrol，但從Fer內容移除preroll

新增類型至AdBreakTimelineItem(AdBreakTimelineItem.placementType)，讓AdPolicySelector可傳回前段、中段和後段內容的不同原則。

* Zendesk #17665 —— 頻寬調節

修正是移除邏輯，以在緩衝開始時將目標緩衝區大小變更為初始緩衝區大小。

**版本1.14.14** (1.4.14.771)

* Zendesk #17363 —— 修正參考播放器的自述檔案

   * 釐清下載和安裝playerglobal.swc的指示。
   * 新增使用特定flash player版本更新專案設定的指示。
   * 更新AdvertisingOverlay專案設定，以使用最低播放器版本。
   * 更新ReferenceCore專案設定以使用特定播放器11.9版

* Zendesk #17471 —— 播放器凍結

部分修正廣告在搜尋後從頭開始無法播放的問題。

* Zendesk #17496 —— 在DVR視窗中尋找時，播客器無法解決

提供每個廣告插播的自訂參數。

**1.4.13版** (1.4.13.660)

* Zendesk #4037 —— 無可用配置檔案錯誤(需要18.0.0.232或更高版本的Flash Player)

修正查詢參數包含&quot;http&quot;時的URL剖析問題

* Zendesk #4260 - IE11中的Flash Player18當機(需要Flash Player18.0.0.232或更高版本)

已修正使用IE11在全螢幕模式中播放視訊時的當機問題

* Zendesk #4262 -Adobe Primetime播放器在Windows 10上當機(需要Flash Player18.0.0.232或更高版本)

已修正在Windows上使用FireFox以全螢幕模式播放視訊時的當機問題。

* Zendesk #4279 - HLS TVSDK廣告插入-iOS和案頭上的302重新導向問題

修正URL無法正確識別其類型，因為沒有副檔名的問題

* Zendesk #4306 —— 僅在Win上全螢幕播放時發生Flash Player崩潰(需要Flash Player18.0.0.232或更高版本)

已修正在Windows上以全螢幕模式播放視訊時的當機問題。

* Zendesk #4480 —— 遺失ID3標籤事件(需要18.0.0.232或更高Flash Player)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增強：處理特定媒體檔案URL中的動態元素。

更新Creative重新封裝服務，以使用動態創意URL正確處理廣告。

* PTPLAY - 2114 - MP4播放支援。

現在支援基本播放MP4內容，包括播放、暫停和搜尋。

以下要求18.0.0.225或更高Flash Player:

* Zendesk #3992 —— 額外的TrickPlay速度。

TrickPlay現在接受高於16倍的費率：+/- 32、+/-64和+/-128。

* Zendesk #3113 -Flash Player插件當機

已修正嘗試在Mac Firefox上播放重新導向廣告時的當機問題。

* Zendesk #4037 —— 無可用配置檔案錯誤
* Zendesk #4262 - Windows 10上的Adobe Primetime播放器當機

已修正在全螢幕播放期間，Windows Firefox中當機的問題。

**1.4.11版** (1.4.11.648)

* Zendesk #1869 —— 問題更改字型大小(需要Flash Player18.0.0.200)

允許在WebVTT標題代碼中使用標題大小。

* Zendesk #3113 -Flash Player插件崩潰(需要Flash Player18.0.0.200)
* Zendesk #3268 —— 台式機：視訊播放器在+- 40/50秒後開始閃爍，在+- 90秒後開始變黑(需要Flash Player18.0.0.200)

修正舞台影片錯誤。

* Zendesk #3670 —— 在參考播放器中搜尋時，VOD中出現INVALID_PARAMETER錯誤(需要Flash Player18.0.0.200)

檢測到新時段時，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 -Flash Player當機，Stream Integrity設為ON on Chrome(需要Flash Player18.0.0.200)

已修正Pepper中原生網路模式的當機問題

* Zendesk #3905 —— 在CDN上代管時，TVSDK播放器不會載入

修正當pageDomain與swf網域不同時，尋找萬用字元的問題。

**1.4.10版** (1.4.10.642)

* Zendesk #3249 - Firefox上的TVSDK Web Player當機Flash

修正當串流在外部螢幕上播放時，切換至較高位元速率串流時，Mac上Firefox偶爾會發生Flash Player當機的問題。(需要18.0.0.160Flash Player)

* Zendesk #3268 —— 台式機：視訊播放器在`+-` 40/50秒後開始閃爍，在`+-` 90秒後開始變黑

修正Mac Chrome上，串流會開始閃爍，最終變成黑色的問題。 (需要18.0.0.161Flash Player)

* Zendesk #3304 —— 未填充VAST 3.0 `[ERRORCODE]`宏

   * 如果內嵌廣告的創意不佳，則會公開錯誤代碼400。
   * `[ERRORCODE]` 巨集將是URL編碼

* Zendesk #3601 —— 增強請求：包裝函式使用者管理

   * TVSDK會將包含資源（html、iframe或static）的包裝函式附屬內容顯示為關閉至內嵌。 （如果內嵌不包含該大小的內嵌）
   * 具有資源的封套，除非用於顯示，否則將忽略。 （不用於跟蹤）
   * 只有具有NO資源的包裝函式伴侶才會用於追蹤目的。 （包含追蹤的包裝函式使用者）

**1.4.9版**

* Zendesk #2615 —— 從台式機顯示器移除HLS視圖的問題

已新增clearVideo()方法至MediaPlayer。 清除StageVideo物件中的AVStream，以清除顯示的視訊影格。 只有在暫停視訊時才應呼叫，且必須先呼叫replaceCurrentResource或replaceCurrentItem，才能再次呼叫play()。

* Zendesk #3169 —— 更新參考播放器並整合Adobe Analytics

參考播放器已更新，已與Adobe Analytics整合

* Zendesk #3296 - Desktop HLS TVSDK - VAST第三方廣告未播放

HLS格式的MIME類型區分大小寫，這是不正確的，而且已經更改，因此不再區分大小寫

**1.4.8版**

* Zendesk #2737 - Desktop Player - Error 106000(需要Flash Player17.0.0.184)
* Zendesk #3007 —— 更新至Flash Player17後未顯示預播廣告(需要Flash Player17.0.0.184)
* Zendesk #3085 - Desktop HLS Player Througs 106000 Error after 60 seconds(需要Flash Player17.0.0.184)

**1.4.7版**

* Zendesk #2760 —— 在TrickPlay模式期間忽略的DINSTRUCTION標籤(需要Flash Player版本17.0.0.158)
* Zendesk #2760 —— 在TrickPlay模式期間忽略的DINSTRUCTION標籤(需要Flash Player版本17.0.0.158)

**1.4.6版**

* Zendesk #2652 - Auditude案頭HLS檔案，Clarified Auditude media_id案頭HLS檔案

**1.4.5版**

* Zendesk #2256 —— 存取主播放清單，更新PSDK，為主播放清單上的訂閱標籤分派timedMetadata事件。 (需要Flash Player版本17.0.0.134)
* Zendesk #2417 —— 播放器嘗試在播放開始前下載字幕，WebVTT使用錯誤的區段編號變數來比對區段編號。 只有區段索引從零開始的媒體才會顯示錯誤。 (需要Flash Player版本17.0.0.134)
* Zendesk #2537 -Flash播放器在搭配Chrome使用胡椒外掛程式時當機(需要Flash Player版本17.0.0.134)
* Zendesk #2547 —— 阿拉伯文字幕：文字應對齊右對齊(需要Flash Player17.0.0.134版)

**1.4.4版**

* Zendesk #1561 —— 續：`[Adobe Primetime]`更新：HLS客戶端在案頭PSDK中對PROGRAM-DATE-TIME的故障切換支援(需要Flash Player版本16.0.0.305或更高版本)
* Zendesk #2197 - `[Ads]`追蹤廣告錯誤
* Zendesk #2286 —— 功能要求：提供廣告載入狀態(VPAID)的資訊
* Zendesk #2285 —— 功能要求：在指定的逾時期間後略過廣告
* 錯誤#3921755 - OpenSSL程式庫在Flash Player中更新至1.0.1L版(需要Flash Player版本16.0.0.305或更新版本)

**1.4.2版**

* Zendesk #1303 —— 隱藏字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，預期發行日期：（2014年12月）
* Zendesk #1870 —— 關閉字幕開啟和關閉(需要Flash Player版本16.0.0.235或更高版本，預期發行日期：（2014年12月）
* Zendesk #2110 —— 在VPAID廣告期間嘗試進入全螢幕後，播放會卡住(需要Flash Player版本16.0.0.235或更高版本，預期發行日期：（2014年12月）
* Zendesk #2199 - `[VPAID]`播放器在搜尋過去廣告插播時未回應
* Zendesk #2358 —— 續：`[Analytics]`章節資料不正確

**1.4.1版**

* 更新封鎖期API以與Android和iOS實作一致。

**1.4.0版**

* Zendesk #1024 —— 透過資訊清單從串流移除廣告的功能
* Zendesk #1423 - HLS回放故障正在鎖定Flash Player（未報告錯誤）
* Zendesk #1674 - ClosedCaption未顯示，當0x03 ETX代碼遺失時，708標題顯示正確。

## 已知問題{#known-issues}

* 隱藏字幕無法處理純音訊內容，因為字幕系統需要視訊才能運作。
沒有視訊，就沒有視訊區尺寸，沒有視訊區尺寸，就無法顯示標題的任何圖形。
* 由於Chrome沙盒限制，Google Chrome中的串流完整性稍慢。
* 在TVSDK 1.4中，如果您停用autoPlay，當播放器閒置至少一分鐘時，可能會發生DRM錯誤。 若要解決此問題，當您停用autoPlay但預先載入資產時，請變更`onPlaybackManagerPrepared`的內容以修改`ReferenceCore.as`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **1.4.13** PTPLAY-8501版——當VMAP傳回兩個直接MP4非轉碼廣告時，相同的回落廣告會播放兩次。

* **1.4.2版** 在Flash Player第16版中，播放器進入空緩衝事件後，ABR「關閉」邏輯發現問題。此問題可防止位元速率在播放器進入緩衝狀態後，在頻寬不佳的環境中關閉。 若要解決此問題，請讓您的應用程式在緩衝狀態期間（即在`BufferEvent.BUFFERING_BEGIN`事件上）將`BufferControlParameters.initialBufferTime`暫時設定為與`BufferControlParameters.playbackBufferTime`相同，然後將它重設回`BufferEvent.BUFFERING_END`事件上的設定值。 此問題的修正將在Flash Player第16版的下一版修補程式中提供。

* **1.4.0版**

   * PTPLAY-1634 —— 相同的「已訂閱」標籤在不同即時視窗中有不同的時間戳記。 當即時視窗移動時，每個視窗中的相同標籤都應有相同的時間戳記。 但是，有時相同的標籤會有不同的時間戳記。
   * PTPLAY-28 - MediaPlayer時間軸不包含空分頁。
   * 需要跨網域原則檔案(crossdomain.xml)，才能取得從不同網域串流內容的權限。 [為HTTP串流設定crossdomain.xml檔案](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)。
   * 錯誤#3694203 —— 在DVR串流中，從播放的中段視訊中搜尋至另一個中段視訊廣告提示可能會導致瀏覽器凍結
   * 錯誤#3753725 - selectPolicyForSeekIntoAd若已觀看廣告分段，則不會考慮
   * 錯誤#3754529 —— 在即時DVR串流中尋找回來時，不會從串流中移除前段廣告
   * 錯誤#3761896 —— 如果廣告播放期間允許搜尋，廣告標籤會在搜尋後重新調整。 解決方法是在搜尋期間不使用ITEM_UPDATED回呼
   * 錯誤#3779889 —— 在視訊分析中，當特技播放達到結束時，未進行完整呼叫
   * 錯誤#VA-779 —— 使用心率支援參考實作的增強視訊分析不會傳送位元速率變更事件心率——特技播放不會在範例應用程式中實作。

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。
