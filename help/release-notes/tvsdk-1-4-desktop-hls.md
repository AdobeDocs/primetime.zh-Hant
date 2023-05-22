---
title: 《 TVSDK 1.4 for Desktop HLS發佈說明》
description: 《 TVSDK for Desktop HLS Release Notes》（台式機HLS發行說明）描述了TVSDK DHLS中的新增或更改內容、已解決和已知問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 5e227c99-acf6-4b16-a35a-68e2928fdbfd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5195'
ht-degree: 0%

---

# 《 TVSDK 1.4 for Desktop HLS發佈說明》 {#tvsdk-for-desktop-hls-release-notes}

《 TVSDK for Desktop HLS Release Notes》（台式機HLS發行說明）描述了TVSDK DHLS中的新增或更改內容、已解決和已知問題。

## 新功能 {#new-features}

**1.4.31**

* **CRS廣告的多CDN支援**

   * 預設情況下，所有轉碼資產都將托管在Akamai上Adobe擁有的CDN上。 在最新版本中，Adobe創意重新打包服務(CRS)提供了將轉碼創意上傳到客戶指定的多個CDN的能力。
   * 將新API添加到TVSDK，以在不使用預設URL時啟用指定最終的CRS建立URL。 請參閱文檔以瞭解如何使用這些新API。

### 以前版本中的新功能 {#new-features-previous}

**1.4.30**

* **計費度量**

為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。

**1.4.24**

* **永久網路連接**

重要提示：必須至少安裝AdobeFlash Player版本22或更高版本。
持久網路連接建立並儲存可重複用於多個請求的網路連接的內部清單，而不是為每個網路請求開啟新連接。 持久網路連接應提高網路代碼的效率並減少延遲。

在此版本中，AppleSafari和Mac上的Mozilla Firefox不支援此功能。

**1.4.19**

* 流完整性支援VPAID廣告。
* 通過解決掛起問題，為Firefox 42及更高版本的Flash播放器FP 20.0.0.267啟用了靜音頁籤選項。

**1.4.18**

* 黃金時段台式機HLS TVSDK現在支援VPAID 2.0線性SWF創意，以實現豐富的互動式流中廣告體驗。

**1.4.10**

* **廣告回退，廣告選擇邏輯中的菊花鏈(Zendesk #3103)** 對於啟用回退規則的VAST廣告（建立性）,TVSDK將MIME類型無效的廣告視為空廣告，並嘗試使用備用廣告。 您可以配置回退行為的某些方面。

有關詳細資訊，請參見 [VAST和VMAP廣告的廣告回退](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)。

**1.4.8**

* **視頻心跳庫(VHL)已更新到1.5版**

   * 能夠將帶有視頻啟動和/或視頻/廣告/章節啟動的元資料作為上下文資料發送
   * 網路通信量減少 — 心跳平均減少，大小減小。

**1.4.7**

* **現場個性化支援**

支援Adobe個性化伺服器的內部安裝，以自定義客戶端的個性化請求以轉到其他端點。

**1.4.6**

* **AES加密示例(需要Flash Player版本17.0.0.134)**

現在支援基於樣例的AES加密。

**1.4.2**

* **視頻心跳庫(VHL)更新到1.4.0.1版**

   * 添加了將來自其他SDK或玩家的不同分析使用案例與Adobe Analytics視頻軟體包捆綁在一起的功能。
   * 已通過刪除trackAdBreakStart和trackAdBreakComplete方法優化了廣告跟蹤。 廣告中斷是從trackAdStart和trackAdComplete方法調用中推斷出來的。
   * 跟蹤廣告時不再需要播放頭屬性。

**1.4.0**

* **具有備用內容替換的封鎖信號** 作為1.4 TVSDK更新的一部分，TVSDK現在還支援針對線性內容進行區域封鎖並返回。 TVSDK現在可以並行處理主檔案和備用檔案兩個清單檔案，以便即使在顯示替代程式時也監視封鎖信號。

* **刪除/更換C3廣告** 現在，無需進行額外的準備工作即可將新廣告動態地插入到從C3窗口發出的視頻點播(VOD)資產中。 TVSDK現在提供了一個API來刪除自定義內容範圍並動態插入新廣告。 這種功能強大的新功能在廣播期間直播/線性內容播放時也很有用，並且會立即被拉下來，作為按需內容使用，而沒有適當的時間來「清理」資產。

## 已解決的問題 {#resolved-issues}

>[!NOTE]
>
>我們強烈鼓勵所有使用CRS的TVSDK客戶至少升級到iOS、Android和Desktop HLS上的TVSDK 1.4.32。 此升級將取代現有應用程式實施的直接導入。 升級後，在代理工具（例如，Charles）中檢查CRS建立URL請求，以驗證路徑中的版本是否反映3.1版。比如說，
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**1.4.41版**

* Zendesk #33777 - DHLS分發生成的本地主機令牌SWF已過期。

   正在更新DHLS上PMP演示的本地主機令牌。

### 已解決以前版本中的問題 {#resolved-issues-previous}

**1.4.38版** (891)

* Zendesk #30731 - TVSDK在AdBreak中不播放多個VPAID廣告。

   在AdBreak中修復多個VPAID廣告播放。

* Zendesk #29968 — 雙公告牌。

   當ABR切換發生時，視頻播放器可以重複週期的最後一段。 因此，有時，最後一段預卷重複。 這個已經修復了。

**1.4.35版** (879)

* Zendesk #26058 — 支援本機VPAID事件

**1.4.33版** (873)

* Zendesk #21701 — 發送1401 CRS請求的原始建立URL，而不是規範化的URL。

   已根據CRS後端的要求解決了請求重新打包的URL進行轉碼的問題。
* Zendesk #26197 — 未以所需的顯示解析度重放變形壓縮。

   **注釋**:此問題需要Flash播放器24.0.0.194或更高版本。

   使用縱橫比表中缺少的條目來計算輸出寬度的問題已得到解決。

* Zendesk #26840 — 在IE11 + Windows7上進行第二次嘗試後HDCP檢測失敗。

   **注釋**:此問題需要Flash播放器24.0.0.218或更高版本。

   通過修改AdobeCP的主消息隊列處理來迭代整個隊列，而不是僅僅阻止第一個消息，解決此問題。

* Zendesk #27460 — 新Akamai帳戶無法處理POSTCDN請求。

   新CDN帳戶無法處理POSTCDN請求。 通過更新代碼使cdn.auditute.com廣告請求成為GET而不是POST，解決此問題。
* Zendesk #27619 - Windows 10上的Flash崩潰

   **注釋**:此問題需要Flash播放器24.0.0.218或更高版本。

   通過防止長URL導致的錯誤，解決此問題。

* Zendesk #28218 — 當從恢復點回退時，跟蹤事件不會觸發

   此問題與Zendesk #26592中的問題相同。 當媒體播放器處於VOD流的PREPARED狀態時允許搜索操作的問題已被解決。

**1.4.32版** (867)

* 當回放從恢復點開始時，Zendesk #26592跟蹤事件不會觸發

當恢復點不為零時，代碼未更新前滾和中斷項。 通過添加邏輯在範圍起始時間不匹配時刷新代碼，解決了此問題。

* 第二次播放資#27022時，不會播放Zendesk廣告

陣列方法的異常已修復。

**1.4.30版** (855)

已在此版本中為TVSDK解決了以下問題：

* Zendesk #22898 — 缺少字幕不應導致播放失敗。

**注釋**:此問題需要Flash播放器23.0.0.185或更高版本。

通過允許TVSDK繼續播放，即使清單缺少WebVTT M3U8，並僅註冊一個警告，此問題已得到解決。

* Zendesk #23454 — 未正確處理第三方廣告(VPAID)

通過根據內容ID而不是時間範圍正確處理VPAID廣告來解決此問題。

* Zendesk #24528 - TVSDK賬單使用度量。

重要提示：此問題需要Flash播放器23.0.0.185或更高版本。

* 調整播放器大小期間出現Zendesk # 25432隱藏字幕問題。

重要提示：此問題需要Flash播放器23.0.0.185或更高版本。

字幕顯示紋理映射代碼已固定，以在播放器調整大小期間正確處理坐標。

視頻心跳庫(VHL)已更新到1.5.9版，以解決以下問題：

* Zendesk #23730 — 比特率度量為空

通過跟蹤VideoAnalyticsTracker中的比特率更改，此問題得到瞭解決。

* 已向PTVideoAnalyticsTrackingMetadata添加新API assetDuration，以更新Live/Linear流的資產持續時間。

**1.4.28版** (848)

* Zendesk #25027 - Auditute在台式機版本1.4.27不起作用

通過添加代碼以檢查AUDITUDE_METADATA_KEY，並使AUDITUDE_METADATA_KEY和ADVERTISING_METADATA_KEY可互換，此問題得到瞭解決。

* Zendesk #24428 — 使用TVSDK播放DRM HLS時經常出現緩衝問題

此問題已解決，因為當沒有廣告設定時，TVSDK可以通過消除用於同步廣告插入的時間線上的預滾動廣告保持和即時保留保持來加快處理速度。

* Zendesk #24344 — 禁用WebVTT檔案以縮短啟動時間。

**注釋**:此問題需要Flash參與人23或更高版本。

僅當需要顯示字幕時，才載入WebVTT檔案，從而解決了此問題。

* Zendesk #24994 — 從商業休息返回時，將從播放器上下放隱藏字幕

**注釋**:此問題需要Flash參與人23或更高版本。

虛假的EOC代碼導致字幕顯示消失。 通過強制608字幕代碼RU2、RU3和RU4在當前活動窗口中提供正確的可見性，此問題得到瞭解決。

**1.4.27版** (844)

* Zendesk #21554 — 未為應用程式類型= video/mp4激發TVSDK錯誤信標

通過啟用TVSDK ping無效資產格式上的正確錯誤跟蹤URL，解決此問題。

* Zendesk #23402 — 廣告播放不完整

**注釋**:此問題需要Flash參與人23或更高版本。

在某些請求上遇到404錯誤後，可能會發生崩潰。 通過確保在處理響應時不關閉連接，此問題已得到解決。 該解決方案確保VPAID廣告檔案不會被錯誤計數，因此在下載時不會釋放它們。

* Zendesk #23621 — 在400和404上重試失敗

**注釋**:此問題需要Flash參與人23或更高版本。

已修復在不同配置檔案之間切換時導致DRM元資料損壞的問題。

* Zendesk #23705 — 在AdSund中斷期間凍結視頻廣告

**注釋**:此問題需要Flash參與人23或更高版本。

此問題與Zendesk #23621中的問題相同。

* Zendesk #23905 — 某些廣告中斷在廣告中斷時跳過

**注釋**:此問題需要Flash參與人23或更高版本。

Windows本機網路代碼已修復，以確保連接不會關閉其他連接當前使用的句柄。

* 票證#24029 - HLS FER流不會回放中端.json檔案中的所有中端廣告。

通過允許客戶端在Opportunity實例上單獨設定自定義參數，以便客戶端不必覆蓋OpportunityGenerator，此問題得到瞭解決。

**1.4.26版** (839)

* Zendesk #18854 — 根據CRS規則更新創意選擇邏輯
   * 為基於CRS規則更新創意選擇邏輯提供支援

* Zendesk #22725 — 在Desktop示例應用程式中實現playbackManager.beginPlayback()

   * 通過在從setupVideo()調用方法時在startPlaybackFromFlashVars末尾刪除此冗餘調用來修復

* Zendesk #22807 - SeekManager空引用異常

   * 通過在SeekManager中提供與_dispatcher相關的必要NULL指針保護來修復

* Zendesk #22822 — 使用TVSDK播放清晰的HLS時頻繁緩衝

   * 通過刪除由adSignlingModeOpportunityGenerator（如果沒有ad）生成的初始機會來修復

* Zendesk #23378 — 流完整性塊rules.xml

   * 通過流完整性工作流載入rules.xml檔案來修復

**1.4.24版** (817)

* Zendesk #19851 — 當播放器適應不同的比特率時，它會在新比特率上跳回幾幀，這會讓體驗變得尷尬

**注釋**:此問題需要Flash播放器22.0.0.175或更高版本。

DRM適配器在下載一小部分資料段後被重置的問題沒有得到正確恢復，已經解決。

* Zendesk #20784 — 分析：觸發內容完成即時視頻轉換

通過添加API(trackVideoComplete)來在LINEAR/LIVE視頻跟蹤會話期間手動觸發內容完成，此問題得到瞭解決。

已更新以下庫：

* Zendesk #21643 - VPAID廣告不能全面播放

   * AdobeMobile庫到4.10.0
   * VHL庫到1.5.6
   * VHL-Nielsen圖書館至1.6.7

在播放VPAID廣告時，使用零高度視區填充舞台解決了此問題。

* Zendesk #22110 — 分析：添加h:sc:心跳跟蹤調用的ssl欄位

已修復與SSL相關的問題，並且TVSDK中使用的VHL庫已更新為最新版本。

* Zendesk #22608 — 視頻間歇性顯示黑屏(需要Flash Player22.0.0.175或更高版本)

在自適應比特率期間，在最大比特率限制下，視頻的重新載入會間歇性地顯示黑屏，即使客戶端看到對位置的更新，並且客戶端的行為就像在播放內容一樣。

**1.4.23版** (809)

* Zendesk #2887 — 將廣告規則邏輯應用到TVSDK時，滾動後廣告跳過問題

**注釋**:此問題需要Flash播放器21.0.0.240或更高版本。

在將廣告規則邏輯應用到TVSDK時跳過後滾廣告的問題。

* Zendesk #19863 — 已丟棄VPAID媒體檔案的廣告

如果一個廣大的內聯廣告具有多個媒體檔案，其中VPAID廣告是第一個廣告，則內聯廣告不會為即時流播放。 此問題已通過取出其他媒體檔案來解決。

* Zendesk #21021 — 延遲綁定音頻導致音頻段重複

**注釋**:此問題需要Flash播放器21.0.0.240或更高版本。

音頻重複問題已解決。

* Zendesk #21125 — 提前從即時/線性廣告中退回

**注釋**:此問題需要Flash播放器21.0.0.240或更高版本。

此版本支援在播放廣告前提前從廣告中斷返回到完成。 通過自定義清單標籤指示提前返回。

* Zendesk # 21369延遲綁定音頻導致時間不一致

**注釋**:此問題需要Flash播放器21.0.0.240或更高版本。

已修復的音頻重複問題也解決了此問題。

* Zendesk #21760, 20921 - Seek上的音頻視頻失步。

**注釋**:此問題需要Flash播放器21.0.0.240或更高版本。

音頻重複問題已修復。

* Zendesk #22024 — 運行TVSDK時出錯

參考播放器未播放任何流並且在啟動時引發異常的問題已得到解決。

**1.4.22版** (791)

* Zendesk #17580 — 黃金時段運行時錯誤，代碼3357

**注釋**:此問題需要Flash播放器21.0.0.197或更高版本。

在調用storeVoucher()時正確初始化deviceID所發生的隨機3357錯誤已修復。

* Zendesk #21334 — 第三方廣告請求的TVSDK廣告請求超時值

在此版本中，已添加全局廣告請求超時。

**1.4.21版** (782)

* Zendesk #19580 TVSDK在發送前等待內容解析程式完成 `PTTimedMetadataChangedNotification` 通知

**注釋**:此問題需要Flash播放器21.0.0.182或更高版本。

通過提供設定Ad標籤和添加自定義機會生成器的功能，在案頭參考播放器中解決了此問題，該生成器顯示如何訂閱自定義提示以及如何在VOD檔案中處理這些提示。

* Zendesk #20806在交換攝像頭後，DVR窗口中的未來中間卷廣告不會觸發

**注釋**:此問題需要Flash播放器21.0.0.182或更高版本。

通過更新應用程式以設定_resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;)，以禁用PIP交換中的預滾動插入，因此不會生成預滾動機會，解決此問題。

引入排序功能來修復因主內容持續時間過長而導致的不順序廣告投放。

* 森德克#20522:無法跳過VPAID 2.0廣告

**注釋**:此問題需要Flash播放器21.0.0.182或更高版本。

* 在廣告寬免期間跳過VPAID廣告，從而解決了這一問題。
* 當adbreak策略設定為跳過時，仍然會調度ad和ad break事件。 玩家狀態不一致。

已解決此問題，以便在跳過廣告中斷時正確行事，而不派送事件。

* Zendesk #20955通過機會生成器在customParameters屬性中設定鍵值對

**注釋**:此問題需要Flash播放器21.0.0.182或更高版本。

在建立廣告請求廣告單元時，Auditude Request會解析自定義參數的AuditudeSettings。

此行為已更改為在請求中包括來自Opportunity對象的自定義參數。 此外，不能在一個Auditude請求中打包具有不同定制參數的多個機會。

* Zendesk #21227 - m3u8無法一致地播放

**注釋**:此問題需要Flash播放器21.0.0.211或更高版本。

通過允許TVSDK忽略包含TVSDK不支援的AC3編解碼器（環繞）的清單（HLS子配置檔案），此問題得到瞭解決。

**1.4.20版** (762)

* Zendesk #19181 — 快速進行特技播放以鎖定流。

**注釋**:此問題需要Flash播放器20.0.0.306或更高版本。

* Zendesk #19286 — 在FER流中來回尋找時發生Flash Player崩潰。

**注釋**:此問題需要Flash播放器20.0.0.306或更高版本。

在GoogleChrome中查找時偶爾出現的掛起通過關閉查詢得到解決，如果查詢需要太長時間才能獲得響應，或者套接字正在關閉。

* Zendesk #19305 — 播放帶有A/V不連續的流時遇到波動播放。

**注釋**:此問題需要Flash播放器20.0.0.306或更高版本。

此問題已通過報告警告而解決。

* Zendesk # 19359 -Flash Player因位於#EXT-X-FAXS-CM而崩潰：集級別清單中的屬性。

當#EXT-X-FAXS-CM標籤出現在播放清單中各個比特率或段之前的頂部播放清單上時，此問題就得到瞭解決。

* Zendesk #19489 — 快速轉發到Live Point停止插件（即時流）

此問題與Zendesk #19181相同。

* Zendesk #19699 - TVSDK無法在WebVTT字幕軌道之間切換

通過在軌道更改時進行播放器轉儲並重新載入清單，並糾正影響雙位元組WebVTT字幕軌道名稱的UTF8字串轉換問題，解決此問題。

**1.4.19版** (1.4.19.738)

* Zendesk #18234 -Flash Player崩潰，在CC中使用Unicode字串回放流

此問題需要Flash PlayerFP 20.0.0.267或更高版本，並通過正確處理Unicode字串來解決。

* Zendesk #18304 — 流完整性支援VPAID廣告

此功能需要Flash PlayerFP 20.0.0.267或更高版本，並已在1.4.19版中引入。

* Zendesk #18766 — 引用播放器無法在CC磁軌名稱中顯示非拉丁文Unicode字元

此功能需要Flash PlayerFP 20.0.0.267或更高版本，並且通過正確處理Unicode字串來修復。

* Zendesk #18804 - Firefox 42中的播放器崩潰

此問題需要Flash PlayerFP 20.0.0.235或更高版本，與Zendesk #18723相同。

* Zendesk #18864 -Flash Player完全插件崩潰

此問題需要Flash PlayerFP 20.0.0.235或更高版本，與Zendesk #18723相同。

* Zendesk #18998 — 如果音頻和視頻時間戳不匹配，則會出現斷續段的無休止下載。

此問題通過忽略時間戳之間的差距和僅播放下載的內容而得到解決。

* Zendesk #19093 — 只有通過實況和全場重播(FER)內容觀看一次中檔廣告，但是當快速轉發或通過廣告尋找時，不能再觀看這些廣告

在Gimphire的預設adPolicy選擇器中，如果觀看中間卷廣告，則在您完成查找時不會將adBreak移到查找位置。 要再次播放廣告，在搜索後，應用程式需要覆蓋selectAdBreaksToPlay()函式。

* Zendesk #19101 — 重新捲入未解決的Midroll廣告將刪除廣告位置。

通過允許播放器更新playbackMetrics時間、minimumOpportunityTime和時間軸，此問題得到瞭解決。

* Zendesk #19102 - FER和特技模式問題

此問題需要Flash PlayerFP 20.0.0.267或更高版本，並通過正確設定advertisingMetadata.adSignlingMode來解決。

* Zendesk #19175 — 有時，在首次播放流時，前滾廣告不會顯示。

通過將新API adRequestTimeout添加到AuditudeSettings中以解決此問題。 用戶現在可以覆蓋預設的10秒廣告請求超時。

**1.4.18版** (1.4.18.722)

* Zendesk #3324 — 當VMAP中沒有廣告媒體時，黃金時段廣告報告不會跟蹤廣告中斷。

當廣告中斷為空時，廣告中斷開始和完整跟蹤事件未被ping通。 通過在空廣告中斷（如VMAP AdBreak）上發送廣告中斷開始ping（使用有效的AdSource節點），解決此問題。

**1.4.17版** (1.4.17.702)

* Zendesk #17168 — 切換可見性後，字幕在10秒左右內不出現

通過為vtt字幕檔案提供EXT-X-MEDIA-TIME標籤支援，此問題得到瞭解決。

* Zendesk #17983 — 未能下載清單的任何鍵，導致整個清單播放失敗

**注釋**:您必須至少具有Flash PlayerFP 19.0.0.245或更高版本。

有時播放即時內容時，清單中可能存在無效的鍵（例如，對於封鎖期），但其他時間範圍可能具有有效的鍵，並且仍將播放。 以前，當清單中列出的密鑰無法下載時，整個清單失敗。 現在，只有當無法下載所有列出的密鑰時，清單才會失敗。 如果某些密鑰有效，但無法下載其中的某些密鑰，則內容將播放。 如果我們嘗試播放一個需要一個我們沒有的密鑰的段，我們仍然會失敗。

* Zendesk #18554 — 在某些情況下，流完整性會修剪Cookie

**注釋**:您必須至少具有Flash PlayerFP 19.0.0.245或更高版本。

Cookie操作代碼中可能截斷Cookie值的錯誤已修復。

**1.4.16版** (1.4.16.684)

* Zendesk #3732 — 添加對Chrome中代理的支援以實現流完整性(需要Flash PlayerFP 19.0.0.207或更高版本)

這是增強。

* Zendesk #4244 - PTS滾動時的流問題

通過檢測滾動和管理每個負載類型的不連續性而非一般性地解決此問題。

* Zendesk #4487 — 跟蹤線性內容通道

通過線上性流回放會話期間重新初始化視頻心跳跟蹤器，解決此問題。

* Zendesk #17427 -Adobe流完整性無法通過Chrome上的代理運行(Win7)()

**注釋**:該解決方案需要Flash PlayerFP 19.0.0.207或更高版本。

此問題與Zendesk #3732相同。

* Zendesk #17907 - pHLS Live Stream上的滯後與Flash Player19

**注釋**:該解決方案需要Flash PlayerFP 19.0.0.207或更高版本。

通過處理在重新載入即時清單時TS檔案的域發生更改並且下載了兩次檔案的即時流，解決此問題。

* Zendesk #17931 — 開始時已經提供Slate的HLS內容無法回放

**注釋**:該解決方案需要Flash PlayerFP 19.0.0.207或更高版本。

通過在第一個TS檔案的前2秒內處理沒有音頻的流，解決了此問題。

* Zendesk #17934 — 帶Flash19.0.0.185的即時流式處理故障

**注釋**:該解決方案需要Flash PlayerFP 19.0.0.207或更高版本。

該問題通過處理在段邊界上音頻和視頻幀之間的時間交織的即時流來解決。

* Zendesk #17973 — 最新Flash Player19.0.0.185在中端運行期間崩潰

**注釋**:該解決方案需要Flash PlayerFP 19.0.0.207或更高版本。

通過處理中間卷和插入的未混音解決了此問題。 （解析器切換發生，在播放過程中的任何時刻，內容都會過渡到中間廣告，或在廣告播放的中間，等等。）

* Zendesk #18049 — 使用Firefox 42測試版的Flash19崩潰

此問題與Zendesk #17973相同。

**1.4.15版** (1.4.15.678)

* 森德克#4377:由於廣告策略而跳過廣告中斷時觸發AD_BREAK_SKPITED事件。

如果跳過了廣告，則修復程式將添加AD_BREAK_SKPITED。

* Zendesk #4496 — 流完整性：錯誤102100，重定向到標籤化流。

該修復是為了通過TVSDK添加對設定AVNetworkConfiguration屬性useCookieHeaderForAllRequests的支援。

* Zendesk #17179 -Flash播放器在針對加密內容的多個SAP更改上崩潰。

已修復播放某些加密內容時的崩潰。

**注釋**:修復程式需要Flash Player19.0.0.200或更高版本。

* Zendesk #17499 — 如何在觀看後不刪除中間頁，而從中間頁內容中刪除前置頁

已向AdBreakTimelineItem(AdBreakTimelineItem.placementType)添加類型，以便AdPolicySelector可以為前滾、中滾和後滾內容返回不同的策略。

* Zendesk #17665 — 頻寬限制

修復是刪除邏輯，以便在緩衝開始時將目標緩衝區大小更改為初始緩衝區大小。

**1.14.14版** (1.4.14.771)

* Zendesk #17363 — 修復參考播放器的自述檔案

   * 闡明下載和安裝playerglobal.swc的說明。
   * 添加有關使用特定Flash Player版本更新項目配置的說明。
   * 更新AdvertisingOverlay項目配置以使用最低播放器版本。
   * 更新ReferenceCore項目配置以使用特定播放器版本11.9

* Zendesk #17471 — 播放器凍結

對於廣告在搜索後從頭開始就不播放的問題進行部分修復。

* Zendesk #17496 — 在DVR窗口中重新查找時未解決播客

為每個廣告分段提供自定義參數。

**1.4.13版** (1.4.13.660)

* Zendesk #4037 — 無可用配置檔案錯誤(需要Flash Player18.0.0.232或更高版本)

在查詢參數包含&quot;http&quot;時修復url分析問題

* Zendesk #4260 - IE11中Flash Player18次崩潰(需要Flash Player18.0.0.232或更高版本)

使用IE11在全屏模式下播放視頻時已修復崩潰

* Zendesk #4262 -Adobe Primetime播放器在Windows 10上崩潰(需要Flash Player18.0.0.232或更高版本)

在Windows上使用FireFox以全屏模式播放視頻時已修復崩潰。

* Zendesk #4279 - HLS TVSDK廣告插入 — iOS和案頭上的重定向問題

修復了URL未正確識別其類型的問題，因為它沒有副檔名

* Zendesk #4306 — 僅在Win上全屏運行時Flash Player崩潰(需要Flash Player18.0.0.232或更高版本)

已在Windows上以全屏模式播放視頻時修復了崩潰問題。

* Zendesk #4480 — 缺少ID3標籤事件(需要Flash Player18.0.0.232或更高版本)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI和CRS |增強：處理某些媒體檔案URL中的動態元素。

更新的Creative Repackaging Service以正確處理使用動態Creative URL的廣告。

* PTPLAY - 2114 - MP4播放支援。

現在支援MP4內容的基本播放，包括播放、暫停和查找。

以下要求Flash Player18.0.0.225或更高：

* Zendesk #3992 - TrickPlay的附加速度。

TrickPlay現在接受高於16倍的速率：+/- 32、+/-64和+/-128。

* Zendesk #3113 -Flash Player插件崩潰

已修復嘗試在MacFirefox上播放重定向廣告時的崩潰。

* Zendesk #4037 — 無可用配置檔案錯誤
* Zendesk #4262 -Adobe Primetime播放器在Windows 10上崩潰

已修復在全屏播放期間在Windows Firefox中崩潰。

**1.4.11版** (1.4.11.648)

* Zendesk #1869 — 更改字型大小問題(需要Flash Player18.0.0.200)

允許在WebVTT標題代碼中使用標題大小。

* Zendesk #3113 -Flash Player插件崩潰(需要Flash Player18.0.0.200)
* Zendesk #3268 — 台式機：視頻播放器在+- 40/50秒後開始閃爍，在+- 90秒後開始變黑(需要Flash Player18.0.0.200)

修復舞台視頻錯誤。

* Zendesk #3670 — 在參考播放器中查找時VOD中出現INVALID_PARAMETER錯誤(需要Flash Player18.0.0.200)

檢測到新時段時，ThreadSeek中的InvalidateProfiles。

* Zendesk #3896 -Flash Player崩潰，Chrome上的流完整性設定為ON(需要Flash Player18.0.0.200)

在Pepper的本機網路模式下固定崩潰

* Zendesk #3905 — 在CDN上托管時不載入TVSDK播放器

當pageDomain與swf域不同時，查找通配符標籤的問題已修復。

**1.4.10版** (1.4.10.642)

* Zendesk #3249 - Firefox上的TVSDK Web Player崩潰Flash

在Mac上，當在外部顯示器上播放的流切換到較高比特率的流時，修復了偶爾使用火狐的Flash Player崩潰。(需要Flash Player18.0.0.160)

* Zendesk #3268 — 台式機：視頻播放器在 `+-` 40/50秒後開始黑 `+-` 90秒

已修復MacChrome上的問題，其中流開始閃爍，最終變黑。 (需要Flash Player18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填充宏

   * 如果內聯廣告的創作性不佳，則將顯示錯誤代碼400。
   * `[ERRORCODE]` 宏將是URL編碼

* Zendesk #3601 — 增強請求：包裝器配套管理

   * TVSDK將顯示包含資源（html、iframe或static）的包裝附件，該附件將關閉到內聯。 （如果內聯不包含該大小的內聯）
   * 將忽略具有資源的封裝伴，除非用於顯示。 （不用於跟蹤）
   * 只有具有NO資源的包裝器伴將用於跟蹤目的。 （僅包含跟蹤的包裝子）

**1.4.9版**

* Zendesk #2615 — 從案頭顯示中刪除HLS視圖時出現問題

已將clearVideo()方法添加到MediaPlayer。 通過從StageVideo對象中清除AVStream來清除顯示的視頻幀。 僅當視頻已暫停時才應調用，並且必須在再次調用play()之前調用replaceCurrentResource或replaceCurrentItem。

* Zendesk #3169 — 使用Adobe Analytics整合更新參考播放器

參考播放器已更新為Adobe Analytics整合

* Zendesk #3296 — 案頭HLS TVSDK — 未播放的廣播第三方廣告

HLS格式的mime類型區分大小寫，這不正確，並且已更改，因此不再區分大小寫

**1.4.8版**

* Zendesk #2737 — 案頭播放器 — 錯誤106000(需要Flash Player17.0.0.184)
* Zendesk #3007 — 更新到第17號Flash Player後未出現預卷廣告(需要Flash Player17.0.0.184)
* Zendesk #3085 - Desktop HLS Player在60秒後拋出106000錯誤(需要Flash Player17.0.0.184)

**1.4.7版**

* Zendesk #2760 — 在TrickPlay模式期間忽略的DINECTION標籤(需要Flash Player版本17.0.0.158)
* Zendesk #2760 — 在TrickPlay模式期間忽略的DINECTION標籤(需要Flash Player版本17.0.0.158)

**1.4.6版**

* Zendesk #2652 — 台式機HLS的審核文檔，Clarified Auditude media_id for desktop HLS文檔

**1.4.5版**

* Zendesk #2256 — 訪問主播放清單，更新PSDK以為主播放清單上訂閱的標籤調度timedMetadata事件。 (需要Flash Player版本17.0.0.134)
* Zendesk #2417 — 播放器在播放開始前嘗試下載字幕，WebVTT使用了錯誤的段號變數來匹配段號。 只有段索引從零開始的介質才會出現Bug。 (需要Flash Player版本17.0.0.134)
* Zendesk #2537 — 使用帶Chrome的胡椒插件時Flash播放器崩潰(需要Flash Player版本17.0.0.134)
* Zendesk #2547 — 阿拉伯文字幕：文本應右對齊(需要Flash Player版本17.0.0.134)

**1.4.4版**

* Zendesk #1561 - Re: `[Adobe Primetime]` 更新：HLS客戶端對案頭PSDK中PROGRAM-DATE-TIME的故障轉移支援(需要Flash Player版本16.0.0.305或更高版本)
* 森德克#2197 - `[Ads]` 跟蹤廣告錯誤
* Zendesk #2286 — 功能請求：提供有關廣告載入狀態(VPAID)的資訊
* Zendesk #2285 — 功能請求：在指定超時持續時間後跳過ad
* 錯誤#3921755 -Flash Player中的OpenSSL庫更新到1.0.1L版(需要Flash Player16.0.0.305或更高版本)

**1.4.2版**

* Zendesk #1303 — 隱藏字幕的垂直偏移(需要Flash Player版本16.0.0.235或更高版本，預期發佈日期：2014年12月)
* Zendesk #1870 — 關閉字幕開啟和關閉(需要Flash Player版本16.0.0.235或更高版本，預期發佈日期：2014年12月)
* Zendesk #2110 — 在VPAID廣告期間嘗試輸入全屏後，播放卡滯(需要Flash Player版本16.0.0.235或更高版本，預期發佈日期：2014年12月)
* 森德克#2199 - `[VPAID]` 玩家在尋找過去廣告中斷時沒有響應
* Zendesk #2358 - Re: `[Analytics]` 章節資料不正確

**1.4.1版**

* 更新的封鎖期API與Android和iOS實現一致。

**1.4.0版**

* Zendesk #1024 — 通過清單從流中刪除廣告的功能
* Zendesk #1423 - HLS回放失敗正在鎖定Flash Player（未報告錯誤）
* Zendesk #1674 - ClosedCaption未顯示，當0x03 ETX代碼丟失時，將正確顯示708標題。

## 已知問題 {#known-issues}

* 由於字幕系統需要視頻才能工作，因此隱藏字幕無法處理僅音頻內容。
沒有視頻，就沒有視區尺寸，沒有視區尺寸，就無法顯示字幕的任何圖形。
* 由於Chrome沙箱限制，GoogleChrome中的流完整性稍慢。
* 在TVSDK 1.4中，如果禁用自動播放，當播放器保持空閒至少一分鐘時，可能會出現DRM錯誤。 要解決此問題，請在禁用自動播放但預載入資產時，修改 `ReferenceCore.as` 通過改變 `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **1.4.13版** PTPLAY-8501 — 當VMAP返回兩個直接MP4非轉碼廣告時，相同的後退廣告播放兩次。

* **1.4.2版** 在Flash Player版本16中，在播放器進入空緩衝事件後，用ABR「關閉」邏輯標識了問題。 當播放器進入緩衝狀態後，該問題防止了在壞頻寬環境中的比特率切換。 要解決此問題，請讓您的應用設定 `BufferControlParameters.initialBufferTime` 等於 `BufferControlParameters.playbackBufferTime` 在緩衝狀態(即，在 `BufferEvent.BUFFERING_BEGIN` 事件)，然後將其重置回設定值 `BufferEvent.BUFFERING_END` 的子菜單。 此問題的修復將在Flash Player版本16的下一個修補程式版中提供。

* **1.4.0版**

   * PTPLAY-1634 — 同一訂閱標籤在不同的即時窗口中具有不同的時間戳。 當即時窗口移動時，每個窗口中的相同標籤應具有相同的時間戳。 但是，有時，相同的標籤具有不同的時間戳。
   * PTPLAY-28 - MediaPlayer時間軸不包括空斷點。
   * 需要跨域策略檔案(crossdomain.xml)才能允許從不同域流式傳輸內容。 [為HTTP流設定crossdomain.xml檔案](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)。
   * 錯誤#3694203 — 在DVR流中，從播放中間卷內查找到另一個中間卷廣告提示可能會導致瀏覽器凍結
   * 錯誤#3753725 — 如果廣告中斷已被監視，則selectPolicyForSeekIntoAd不會考慮
   * 錯誤#3754529 — 在即時DVR流中尋回時，不會從流中刪除預滾廣告
   * 錯誤#3761896 — 如果在廣告播放期間允許搜索，則廣告標籤將在搜索後重新調整。 解決方法是在查找過程中不使用ITEM_UPDATED回調
   * 錯誤#3779889 — 在視頻分析中的特技播放結束時，不會發出完整呼叫
   * 錯誤#VA-779 — 不會為具有心跳支援參考實施的增強視頻分析發送比特率更改事件心跳 — 在示例應用程式中不實現特技播放。

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
