---
title: iOS適用的TVSDK 3.13發行說明
description: iOS適用的TVSDK 3.13發行說明說明TVSDK iOS 3.13的新增或變更專案、已解決和已知問題以及裝置問題。
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# iOS適用的TVSDK 3.13發行說明 {#tvsdk-for-ios-release-notes}

iOS適用的TVSDK 3.12發行說明說明TVSDK iOS 3.12的新增或變更專案、已解決和已知問題以及裝置問題。

## 系統和軟體需求 {#system-software-requirements}

下載iOS 3.12之前，請確認您的硬體、作業系統和應用程式版本符合下列需求：

作業系統： iOS 8.0或更新版本。

## iOS TVSDK 3.13

此發行版本引入了對適用於即時、VOD和FER資料流的「HLS/CMAF」（前置、中置和後置）廣告的支援。

如需客戶回報問題的修正，請參閱 [已解決的問題](#resolved-issues). 如需限制，請參閱 [已知問題和限制](#known-issues-and-limitations).

### 舊版新功能和修正 {#whats-new-previous}

**iOS TVSDK 3.12**

修正播放15分鐘後即時資料流失敗的問題。

**iOS TVSDK 3.11**

針對下列客戶問題提供修正： `isFallbackOnInvalidCreativeEnabled` 和方法 `customParams` 導致應用程式當機。

**iOS TVSDK 3.10**

* 修正TVSDK播放器無法引發的問題 `PTMediaPlayerStatusError` 網路無法使用時通知。

**iOS TVSDK 3.9**

* 修正VTT字幕無法播放而導致應用程式凍結的問題。

* iOS TVSDK 3.9包含更新的個人化傳輸憑證。

**iOS TVSDK 3.8.0.83 Hotfix**

Hotfix已更新個人化傳輸憑證。

**iOS TVSDK 3.8**

iOS 13法規遵循與處理iOS 13 `UIWebView` API淘汰。

**iOS TVSDK 3.7**

當同時提出許多廣告解析請求時播放停止的情況的Hotfix。

**iOS TVSDK 3.6**

**類別的vastXML屬性中的修正`PTNetworkAdInfo`**

此 `vastXML` 屬性未正確設定，且傳回nil值。

**iOS TVSDK 3.5**

**啟用背景音訊**

*設定您的應用程式，以便在進入背景時繼續播放音訊。*

若要啟用此功能，我們必須設定新的API `audioPlaybackInBackground` 已新增至 `PTMediaPlayer` 類別。 啟用此API後，您的應用程式便可播放背景音訊。

**iOS TVSDK 3.4.0.19 (Hotfix)**

此版本已修正廣告容錯移轉案例中發生的應用程式當機問題。

**iOS TVSDK 3.4**

**廣告解析逾時**

* 透過TVSDK 3.4，使用者現在可以為整體廣告解析度和資訊清單下載設定逾時值。 如果在指定的逾時時間內部分廣告仍未解析，TVSDK會播放其餘廣告。

* `PTAdMetadata: adRequestTimeout` API已過時，並將被移除。 預設值已設定為35秒。

* 中引進了兩個新的替代API `PTAdMetadataClass: adResolutionTimeout`   — 整體廣告解析呼叫adManifestTimeout的逾時 — 廣告資訊清單下載的逾時。

**收入最佳化**

啟用TVSDK以識別與廣告插入工作流程相關的問題區域，以報告至所選擇的分析端點。

**版本3.3**

TVSDK 3.3現在與iOS 11 SDK相容。 所有已棄用的API已更換為合適的替代方案。

**版本3.2**

**其他記錄支援（第2階段）**

新增對錯誤通知的支援，適用於下列情況：

* HLS版本的廣告使用比內容更高的層級。

* 僅限音訊的變體已排除。

* VAST/VMAP要求失敗。

**版本3.1**

* **其他記錄支援**
新增在廣告播放失敗時支援描述性通知。

* **已新增 [!DNL Fairplay] 加密的CMAF資料流支援**
   [!DNL Fairplay] 現在支援使用AVC轉碼器播放的加密CMAF資料流。

**版本3.0.1**

此版本中沒有新功能或增強功能。

**版本3.0**

* TVSDK 3.0支援HEVC資料流。

* 即時 — 解決廣告更接近廣告標籤的問題。

已新增 `enableDelayAdLoading` 應用程式層級介面上布林值型別的屬性，以啟用JIT。 若 `enableDelayAdLoading` 否，則會 `setadMetadata.delayAdLoading`True （PTAdMetadata介面的屬性）。

啟用此屬性後，TVSDK會根據定義的公差值，解析位置之前的每個廣告插播。 依預設， `delayAdTolerance` 設為5秒。

**版本1.4.45**

為符合Xcode10，TVSDK已從 `libstdc++` 至 `libc++`，因此支援的最低版本為iOS 7。 之前是iOS 6。

**版本1.4.44**

此版本中沒有新功能或增強功能。

**版本1.4.43**

* 類似電視的體驗，即能夠在廣告中間加入，而不會觸發部分廣告的追蹤。\
   範例：使用者在包含三個30秒廣告的90秒廣告插播中間（在40秒）加入。 這是插播中第二個廣告的10秒。

   * 第二個廣告會播放剩餘的持續時間（20秒），接著是第三個廣告。
   * 未觸發已播放部分廣告（第二個廣告）的廣告追蹤器。 只會觸發第三個廣告的追蹤器。

* 已新增 `enableVodPreroll` PTAdMetadata介面中布林值型別的屬性。 屬性可用來在VoD資料流上啟用前置滾動。 若 `enableVodPreroll` 否，PSDK不會播放前段廣告。 但是，這對中段沒有任何影響。 預設值 `enableVodPreroll` 是。
* `closedCaptionDisplayEnabled` 的API `PTMediaPlayer` 介面從iOS v1.4.43開始標籤為已棄用。 若要判斷隱藏式字幕是否適用於指定的字幕 `PTMediaPlayerItem`，檢查 `subtitlesOptions` 屬性 `PTMediaPlayerMediaItem`.

**版本1.4.42**

此版本中未新增任何新功能。 如需已修正的問題清單，請參閱 [已解決的問題](#resolved-issues).

**版本1.4.41**

API變更：

* **isSecure**：推出新的API isSecure，可保護播放器避免錄製和擲回錯誤。 預設值為true。

* **allowExternalRecording**：引入新API以允許安全內容的播放映象。 因此，播放映象會被視為錄製 `allowExternalRecording` 值必須設定為 `True`，以允許播放映象或設為 `False` 停止安全內容的播放映象。 依預設， `value` 為true。

**1.4.40版**

沒有新功能。

**版本1.4.39**

* iOS TVSDK已通過VHL 2.0.1和VHL 2.0.1的認證，並與Nielsen合作。

* iOS TVSDK已更新，可向新Akamai主機發出CRS請求 `primetime-a.akamaihd.net`.

* 新的主機名稱設定可大幅透過HTTP和HTTPS (SSL)提供CRS資產傳遞。

**版本1.4.36**

在iOS TVSDK中整合及認證VHL 2.0 ：降低 `VideoHeartbeatsLibrary` 降低API的複雜度以利實作。

**版本1.4.34**

**網路廣告資訊**

TVSDK API現在提供有關協力廠商VAST回應的其他資訊。 廣告ID、廣告系統和VAST廣告擴充功能提供於 `PTNetworkAdInfo` 類別可透過  `networkAdInfo`  屬性。 此資訊可用於與其他Ad Analytics平台整合，例如 **Moat Analytics**.

**版本1.4.31**

* **計費量度** 為因應客戶只想依使用量付款，而不想依實際使用量支付固定費率的需求，Adobe會收集使用量度並使用這些量度來決定向客戶收費的金額。

   每當TVSDK產生資料流開始事件時，播放器就會開始定期傳送HTTP訊息至Adobe的計費系統。 期間（稱為可計費期間）在標準VOD、pro VOD （啟用中段廣告）和即時內容中可能不同。 每種內容型別的預設持續時間為30分鐘，但您的Adobe合約會決定實際值。

* **CRS Ads的多重CDN支援** TVSDK現在支援CRS廣告的多重CDN。 透過提供CRS廣告的FTP詳細資料，您可以指定CDN位置，而不是Adobe擁有的預設CDN，例如 [!DNL Akamai].

**版本1.4.29**

在 `PTSDKConfig` 類別， `forceHTTPS` 已新增API。

此 `PTSDKConfig` class提供在向Adobe Primetime ad decisioning、DRM和Video Analytics伺服器提出的請求上強制SSL的方法。 如需詳細資訊，請參閱 `forceHTTPS` 和 `isForcingHTTPS` 此類別上的方法。 如果資訊清單是透過HTTPS載入，TVSDK會保留HTTPS的內容使用方式，並在從該資訊清單載入任何相對URL時遵循此使用方式。

>[!NOTE]
>
>對第三方網域（例如廣告追蹤畫素、內容和廣告URL）的要求以及類似要求不會修改，內容提供者和廣告伺服器有責任提供透過HTTPS支援的URL。

**版本1.4.18**

Primetime iOS TVSDK現在支援VPAID 2.0 JavaScript創意，以提供豐富的互動式串流廣告體驗。 如需VPAID 2.0的詳細資訊，請參閱VPAID廣告支援。

**版本1.4.17**

* tvOS

   tvsdk支援tvOS原生應用程式。
* 可以播放下列型別的內容：

   * VOD
   * 即時
   * AES-128
   * 替代音訊和字幕
   * FER

* 可以顯示下列型別的廣告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 目前不支援下列功能：

   * Digital Rights Management(DRM)
   * 廣告橫幅
   * 電視標籤語言(TVML)

**版本1.4.13**

>[!NOTE]
>
>Nielsen模組已從TVSDK建置版本中移除，TVSDK將很快更新為新的Nielsen整合模組。

**廣告遞補、廣告選擇邏輯中的Daisy鏈結(Zendesk #3103)**

對於已啟用遞補規則的VAST廣告（創意內容），TVSDK會將具有無效MIME型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。 如需詳細資訊，請參閱VAST和VMAP廣告的廣告遞補。

**版本1.4.9**

**使用替代內容取代發出中斷訊號**

在1.4 TVSDK更新中，Adobe現在也支援對線性內容進入和結束地區性中斷後返回。 TVSDK現在可以並行處理兩個資訊清單檔案（主要和替代），以監控中斷訊號，即使替代程式設計正在取代原始程式設計。

**版本1.4.8**

**視訊心率程式庫(VHL)更新至1.5版**

* 能夠連同視訊開始或視訊/廣告/章節開始一起傳送中繼資料作為內容資料。

* 網路流量更少 — 心率平均而言更少，大小也更小。

**版本1.4.7**

* **內部部署個人化支援**

支援Adobe個人化伺服器的內部部署安裝，可自訂使用者端的個人化請求，以移至其他端點。

* **以解析度為基礎的輸出保護**

DRM原則現在可以根據裝置的「輸出保護」功能，指定允許的最高解析度。 例如， _如果有HDCP可用，則允許播放解析度最高為1080p的內容；如果沒有HDCP，則允許播放解析度最高為480p的內容。_

**版本1.4.4**

* **視訊心率程式庫(VHL)更新至1.4.1.1版**

   * 新增將其他SDK或播放器中的不同Analytics使用案例與Adobe Analytics Video Essentials搭配的功能。
   * 廣告追蹤已透過移除 `trackAdBreakStart` 和 `trackAdBreakComplete` 方法。 廣告插播是從 `trackAdStart` 和 `trackAdComplete` 方法呼叫。
   * 此 `playhead` 追蹤廣告時不再需要屬性。
   * 新增對Experience CloudID服務的支援。

* **Nielsen SDK整合**

TVSDK現在支援傳送mTVR和MDPR ID3信標至Nielsen SDK，無需任何自訂整合。 若要開始使用，請下載3.1.2.19 Nielsen iOS應用程式SDK，並按照iOS程式設計師指南中的說明操作。

**1.4.0版**

* **使用替代內容取代發出中斷訊號**

在1.4 TVSDK更新中，TVSDK現在也支援進入及從線性內容的區域中斷返回。 TVSDK現在可以並行處理兩個資訊清單檔案（主要和替代），以監控中斷訊號，即使替代程式設計正在取代原始程式設計。

* **移除/取代C3廣告**

現在，不需要進行額外的準備工作，即可動態地將新廣告插入從C3視窗傳出的隨選影片(VOD)資產。 TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 在廣播期間播放即時/線性內容，並立即下拉以供隨選內容使用（沒有適當的時間清除資產）的情況下，這項強大的新功能也很有用。

## 已解決的問題 {#resolved-issues}

如果解決方法與報告的問題相關聯，則會顯示Zendesk參考，例如ZD#xxxxx。

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085) - CMAF資料流的播放問題。

* (ZD-43215) — 在廣告進行中關閉播放器時當機。

* (ZD 43210) — 啟用WebVTT字幕時，iOS HLS播放凍結。

**iOS TVSDK 3.12**

* 使用iOS 3.10的TVSDK時，即時資料流在播放15分鐘後失敗。

### 舊版中的已解決問題 {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - `isFallbackOnInvalidCreativeEnabled` 導致應用程式當機。

* (ZD#41289) - `NSInvalidArgumentException` 以方法觀察 `customParams` 導致應用程式當機。

**iOS TVSDK 3.10**

(ZD#40943) - TVSDK播放器未觸發 `PTMediaPlayerStatusError` 網路無法使用時通知。

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK無法播放VTT字幕併發101001錯誤，導致應用程式凍結。

**iOS TVSDK 3.8**

* (ZD#40087) - iOS當機，並顯示過期的VOD內容發生播放器錯誤。

* (ZD#40083) — 使用時，前段廣告不會針對直播串流播放 `OpportunityGenerator` 而播放器發生錯誤。

* (ZD#39828) - `CurrentItem` 屬性缺少空值註釋，導致在通知中包含的播放器狀態為時造成播放器當機 `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) — 當設定在PiP中播放多個內容時，一個內容完成播放後，無法在「子母畫面(PiP)」視窗中播放內容。

**iOS TVSDK 3.6**

此版本中沒有新問題。

**iOS TVSDK 3.5**

此版本中沒有新問題。

**版本3.3**

(ZD#37820) — 新增自訂標頭HS-Id、HS-SSAI-TAG的允許清單。

**版本3.2**

* **Ticket#36588**  — 呼叫MediaPlayer STOP方法時會觀察到播放器當機。

修正在一些具有字幕的串流呼叫STOP方法時觀察到的間歇性當機。

* **Ticket#37080**  — 資訊清單呼叫出現重複請求。
修正播放期間對資訊清單URL提出的重複請求。 TVSDK現在會針對每個資訊清單進行一次呼叫。

* **票證#37** - CRS標準化規則失敗，出現eq比對型別修正播放器遇到具有「eq」比對型別之主機名稱的上一個標準化規則集時會發生當機的情況。

**版本3.1**

**票證#36313**  — 線性廣告插播期間的間歇性無法預測的結果在即時資料流中的線性廣告插播期間固定的間歇播放。

**版本3.0.1**

**票證36948** - CRS - iOS 12上資產選擇順序不一致為CRS選擇的資產並不總是在VAST或VMAP回應中傳回的最高品質變體。

**版本3.0**

* **票證35311**  — 在電話中斷期間，播放器狀態不會變成「已暫停」新增中斷處理常式，以停止播放器中斷。 中斷時，播放器狀態會變成「已暫停」，然後按一下播放按鈕以繼續播放。

* **票證36685**  — 即時資產 — 時間與播放器時間進度和SCTE標籤時間不符。系統會針對在即時點之前的SCTE標籤計算正確時間。

* **票證36492** - `currentTime` 和 `localTime` 在暫停狀態期間搜尋新位置時不會更新播放器目前的時間現在可以設為零，以防播放器處於暫停狀態；以前只會將播放狀態的目前時間設為零。

**版本1.4.45**

* **票證36294** - iOS TVSDK無法與Xcode 10搭配使用修正TVSDK在XCode 10上的編譯問題。 由於XCode十大需求，在iOS 1.4.45以上的TVSDK上建置應用程式需要最低部署目標，如iOS 7.0

* **票證36321**  — 可搜尋範圍中發現的差異，介於 `PTMediaPlayer` 和 `AVPlayer` 中的執行個體 _正在播放_ 州別。

* **票證36493** - `libstdc++` iOS 12的支援修正iOS 12上TVSDK的編譯問題。 iOS 1.4.45以上版本的TVSDK上建置的應用程式需要最低部署目標為iOS 7.0

**版本1.4.44**

* **票證34683**  — 廣告播放進度時間將呈負數

當廣告伺服器報告的持續時間與實際廣告內容不符時，會輸入其他檢查來處理這種情況。

* **票證34801** - `currentTime` 和 `localTime` 在暫停狀態期間尋找新位置時未獲得更新播放器的目前時間現在可以設為零，以防播放器處於暫停狀態；以前僅播放狀態的目前時間設為零。

* **票證35037**  — 從訊號型廣告插入傳回時，播放停止並出現錯誤的URL。
1.4.42版中針對已關閉問題#34385案提供的改良修正。 新增isCanceled檢查與例外狀況處理程式碼，讓作業佇列更穩健。

**版本1.4.43**

* (ZD#32990) - iOS：在某些提示點上播放內容而非廣告。 `selectedMediaOptionInMediaSelectionGroup` API是AVPlayerItem介面的一部分，現在已移至 `AVMediaSelection` 在iOS 11中。 此新API已解決問題。

* (ZD#33683) TVSDK已移除 `==` 後置詞。 此問題已在剖析邏輯中修正。

* (ZD#33905) - iOS TVSDK透過兩個使用者代理程式呼叫資訊清單檔案。 使用者代理問題已在第一個m3u8呼叫（全新安裝案例）中修正。 M3u8現在對所有呼叫具有相同的使用者代理。

* (ZD#34293) — 插入在LINEAR資料流上的前段膠捲無法在iOS11上正確播放。 前段廣告的問題已修正。

* (ZD#34684) — 套用廣告略過原則時，前段廣告框架會顯示幾秒。 新API、 `enableVodPreroll` 引入以停用vod播放中的前段播放。 此API的預設值為 _是_. 此API可確保跳過主要內容中的廣告內容拼接。

* (ZD#34765) — 通話後 `stop()`，仍會下載少數「傳輸串流」區段。 增強 `Stop()` 避免下載額外區段的API。

* (ZD#34865) — 前段廣告 [!DNL Livestream] 在iOS上遭截斷。 與iOS11相關，並新增額外檢查以確認串流是前段或主要內容，可解決此問題。

* (ZD#35093) — 修正容錯移轉情況，其中如果資料流的主要變體在啟動時失敗（傳回404），播放不會切換至備份資料流。

**1.4.42 (1.4.42.118)**

* (ZD#34385) — 從訊號型廣告插入傳回時，播放因錯誤URL而停止。

   增加以下專案的最大並行計數： `CustomAVAssetLoaderOperations`，以便資訊清單讀取可以繼續執行。

* (ZD#34373) — 不允許串流錄製時，一般使用者無法串流到HDMI連線的裝置。

* (ZD#32678) - TVSDK無法在iOS上收集正確的廣告ID。

   如果有VAST/VMAP重新導向，VHL Ping現在會擷取最終廣告創意的廣告ID。

* (ZD#33904) - TVSDK未註冊AVFoundation通知 `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` 和 `PTMediaServicesWereResetNotification` 現在可以在播放器應用程式上註冊，以便在媒體服務重設或遺失時取得通知。

* (ZD#33815) — 客戶無法在不更新應用程式的情況下更新其優先順序和標準化CRS規則。

   已新增 `getCRSRulesJsonURL` 和 `setCRSRulesJsonURL` iOS TVSDK的API 。

**1.4.41版(1.4.41.76)**

* (ZD #34464) — 使用TVSDK 1.4.41版建置參考應用程式時發生問題

   自此版本開始，編譯適用於iOS的TVSDK時需要Xcode 9。
* (ZD #29456) — 播放開始於暫停狀態

   修正進入Airplay時視訊暫停的暫停問題。
* (ZD #30371) — 線上性資料流中插入兩個以上的廣告時，廣告插播開始時間會變更

   修正嘗試在Apple TV上播放內容時，導致無法完全播放的錯誤
* (ZD #32146) — 否 `PTMediaPlayerStatusError` 已收到有關封鎖iOS 11 dev beta版的HLS Live內容之資訊

   否 `PTMediaPlayerStatusError` 使用Charles進行封鎖時，收到有關HLS即時和VOD內容的（中斷連線和403）。

* (ZD #29242) — 啟用廣告時，Airplay視訊播放失敗。

   當廣告已啟用且AirPlay已啟用開始播放視訊時，視訊播放不會開始且不會顯示錯誤。

* (ZD#33341) - `DRMInterface.h` 觸發Xcode 9中的組建警告。

   修正中的兩個區塊原型 `DRMInterface.h` 引數清單中遺漏&#39;void&#39;一詞。

* (ZD#31979) — 當它是iPhone 7/iPhone7+的iOS 10或更新版本時，不會編譯/執行。

   已修正不再支援iOS 7之前的編譯IB檔案。

* (ZD#32920) — 廣告插播內的空白畫面且沒有廣告插播完成。

   當廣告插播展示廣告例項時，在廣告例項完成後，會顯示空白畫面。

* (ZD#32509) — 停用iOS 11熒幕錄製停用iOS 11上的熒幕錄製。

* (ZD#33179) - iOS11發生間歇性事件失敗。

   修正iOS 11上的事件失敗。

**1.4.40版** (1.4.40.72)

* (ZD #32465) — 播放器無法處理合併的播放清單。

   呼叫 `finishLoadingWithError`（含：錯誤），供AV foundation嘗試替代串流/觸發容錯移轉。

* (ZD #31951) — 授權循環期間發生TVSDK錯誤。

   已修正授權輪換問題。
* (ZD #31951) — 廣告插播內的空白畫面且沒有廣告插播完成。

   處理Facebook VPAID廣告通常在單一中傳回多個CDATA區塊的問題 `<AdParameters>` VAST節點
* (ZD #33336) - iOS TVSDK — 雖然Freewheel傳回的廣告已足夠，廣告匣仍未填滿。

   在序列廣告和遞補廣告之間建立父子關係，並根據父序列和索引進行排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178) - iOS TVSDK版本不正確。

   記錄檔中的TVSDK版本輸出為1.0.211。輸出正確版本是固定的。

* (ZD #32199) — 延遲廣告載入 — 不針對內容顯示影片。

   先前未初始化的本機Adbreak時間表現在會在使用前重新整理。

* (ZD #27528) — 如果次要音訊在iOS 1.2上設為非預設值，則資產開始播放後1-45秒會凍結視訊、音訊或兩者。

   準備並通知處於就緒狀態的音軌。

* (ZD #30411) — 如果您選擇次要Sap語言，可能會收到未預期的結果，例如沒有音訊或音訊不正確。

   準備並通知處於就緒狀態的音軌。

* (ZD #32199) — 延遲廣告載入 — 不針對內容顯示影片。

   先前未初始化的本機Adbreak時間表現在會在使用前重新整理。

* (ZD #27528) — 如果次要音訊在iOS 1.2上設為非預設值，則資產開始播放後1-45秒會凍結視訊、音訊或兩者。

   準備並通知處於就緒狀態的音軌。

* (ZD #30411) — 如果您選擇次要Sap語言，可能會收到未預期的結果，例如沒有音訊或音訊不正確。

   準備並通知處於就緒狀態的音軌。

**版本1.4.38** (1.4.38.860)

* (ZD #29281) - iOS：將AdSystem和創作Id新增至CRS請求

根據CRS標準化規則在CRS請求中使用創作ID和AdSystem

* (ZD #29176) — 當機於 `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

現在已處理因空白AdBreak而造成的當機。

* (ZD #30125) — 程式化廣告無法在iOS平台中運作

在iOS中新增程式化廣告支援。

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME通知

使用即時DRM資料流的# EXT-X-PROGRAM-DATE-TIME標籤不會觸發定時中繼資料事件。

**1.4.37版(1.4.37.842)**

* (ZD #28950 ) - VOD播放問題

當串流中的# EXT-X-PLAYLIST-TYPE標籤設定為Event而非VOD時的播放問題

* (ZD #29281) - iOS：將AdSystem和創作Id新增至CRS請求

根據CRS標準化規則，在CRS請求中使用Creative Id和AdSystem。

* (ZD #29462) - A&amp;E VOD中的TremorHub廣告導致iOS應用程式當機

**版本1.4.36 (1.4.36.835)**

* (ZD #29418) — 持續時間為0 (#EXT-X-CUE-OUT：0.000)的提示會導致iOS TVSDK停止或當機播放。

問題已修正，且播放已正確開始。

* (ZD #29462) - VOD中的廣告導致iOS TVSDK當機。

問題已修正。 iOS TVSDK正在引發 `exception(AUDNetworkAdInfo::initWithAdId)` 而不處理它。 此例外狀況是因為空白的廣告ID。

* (ZD #29281) — 將AdSystem和Creative ID新增至CRS請求。

將AdSystem和CreativeId加入為1401和1403請求中的新引數（所有其他引數保持不變）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830) — 需要以程式設計方式確定iOS中隱藏式字幕與字幕的差異。

TVSDK現在會顯示兩種型別，可用來篩選掉所需的註解型別。

* (ZD #29160) - TVSDK iOS上未正確插入EXT-X-CUE-OUT廣告提示。

搭配EXT-X-CUE-OUT midroll廣告正在播放中。

* (ZD #29100) — 當使用者拖曳至影片結尾時，應用程式當機。

修正了與同步相關的多次當機。

* (ZD #28785)、 (ZD #27712)和(ZD #25076) - iOS應用程式在大型直播活動期間當機。

修正了與同步相關的多次當機。

**版本1.4.34** (iOS 6.0+為1.4.34.815)

* (ZD #28481) - FER中斷，因為這些FER資料流的廣告插播結尾附加了錯誤的索引鍵

對於FER資料流，會在廣告插播結束之後插入廣告插播之前的索引鍵。 此問題已透過附加 *上次檢視的金鑰* 在廣告插播結束時。

**版本1.4.33** (iOS 6.0+為1.4.33.803)

* (ZD# 21701)為子帳戶啟用CRS

根據CRS後端的需求，透過傳送1401 CRS請求的原始創意URL而不是標準化URL來啟用。

* (ZD# 26218) - `PSDKResources.bundle` 載入問題

此問題已透過更新資源載入以從所有可用套件組合中檢視來解決。

* (ZD# 27460) Midroll第一個廣告呼叫 — POST至 `cdn.auditude.com` 傳回403。

新的CDN帳戶無法處理POST CDN請求。 此問題已透過更新程式碼以使 `cdn.auditude.com` 廣告要求是GET而非POST。

**版本1.4.32** (iOS 6.0+為1.4.32.792)

* (ZD# 27132)支援VMAP廣告插播的小數值。

未依照定義的廣告插播將內容分段時，整數會導致非預期的廣告位置。 未將小數值轉換為整數即可解決此問題。

* (ZD# 27189)具有EXT-X-DISCONTINUITY-SEQUENCE標籤的AES內容無法正確播放。

將標籤放在播放清單的開頭即可解決問題。

**版本1.4.31** (iOS 6.0+為1.4.31.785)

* (ZD# 24528)實作計費的TVSDK使用量度

如需詳細資訊，請參閱 [計費量度].

* (ZD# 24642) TVSDK的畫中畫支援

畫中畫功能有時會無法正常運作，目前已修正。

* (ZD# 25246)不正確的廣告插播訊號

此問題可透過在變體資訊清單間對齊不連續標籤來解決。

* (ZD# 26218)嘗試加入時，應用程式建置流程會變得複雜 `PSDKLibrary.framework` 在使用者端的應用程式架構中

此問題已透過封裝 `PSDKLibrary.framework` 依要求。

* (ZD# 26364) CRS Ads的多重CDN支援

如需詳細資訊，請參閱CRS廣告傳送的多重CDN支援。

* (ZD# 27028)iOS 10中部分資料流的播放延遲。

此問題已藉由為沒有M3U8擴充功能的資料流提供因應措施而解決。

**1.4.30版** (iOS 6.0+為1.4.30.754)

此版本解決了TVSDK的下列問題：

* (ZD# 24180)新增自訂標頭至允許清單。

新的自訂標題已新增至TVSDK允許清單。

* (ZD# 25016)設定ABR控制引數時，會隨機選取容錯移轉資料流

當ABR設定隨附於 `initialBitrate` 在包含容錯移轉URL的資料流上設定。 這樣可避免播放容錯移轉串流而非主要串流。

* (ZD# 25076)當機於 `PTAuditudeAdResolver loadComplete`

已修正快速啟動/停止多個具有廣告的PTMediaPlayer執行個體期間發生當機的問題。

* (ZD# 25960)沒有其他訂閱標籤會觸發中繼資料變更通知廣播

已修正當訂閱標籤出現在資訊清單中的第一個區段之前時，未收到通知的問題。

* (ZD# 26084) PSDK擲回106000.101000.-11833從上一個廣告插播轉換回娛樂內容時，找不到解碼器錯誤

當來自VMAP的最後一個廣告插播開始時間在總持續時間完成之前時，在某些情況下，直到最後一個廣告插播結束之後才會插入索引鍵。 此問題已修正。

* 視訊心率程式庫(VHL)已更新至1.5.9版，以解決下列問題：

* (ZD #22351) VHL - Analytics：即時視訊資產持續時間

此問題已透過新增  `assetDuration`  API至 `PTVideoAnalyticsTrackingMetadata` 更新即時/線性資料流的資產持續時間，並提供檢查即時資料流的邏輯。

* (ZD# 22675) VHL - Analytics：更新即時視訊資產持續時間

此問題與ZD #22351相同。

* (ZD #25908) VHL - Analytics：Adobe心率事件當機

此問題已透過更新實作以使用iOS 1.5.9版適用的最新版VHL來改善穩定性和效能而解決。

* (ZD #25956) VHL - Analytics：重複播放視訊時當機

此問題與ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)未播放協力廠商廣告

移至CRS v3 URL結構，在重新封裝的URL中包含區域ID，即可解決此問題。

* (ZD #25183) tvOS和iOS上的DRM播放問題

此問題已透過提供支援多個DRM支援所需的多個關鍵標籤來解決。

* (ZD# 25334) TVSDK無法播放cDVR共用內容

透過防止TVSDK將空白字串轉換為絕對URL，此問題已解決。

* (ZD# 25347)在AVURLAsset上設定自訂HTTP標頭

透過支援其區段請求上的自訂標頭 `PTNetworkConfiguration` 類別已新增。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多個廣告追蹤呼叫

此問題已透過更新時間表管理員解決，以便在建立多個播放器時接聽特定物件的通知。

* (#24758斐濟元) `PTManifestLogger` 不支援iOS 8

將記錄器公用程式程式庫更新至7.0版部署目標，即可解決此問題。

* (ZD #24775)由於廣告而延遲的資料流

正確計算事件播放清單上的持續時間漂移即可解決此問題。

* (ZD #24799)部分集數未在iOS應用程式中播放

當WebVTT檔案受到地理限制時，此問題可透過使用本機網頁伺服器來製作字幕來解決。

**版本1.4.27** (1.4.27.711) (適用於iOS 6.0+)

* (ZD #24089) — 針對長DVR資料流的廣告解析進行最佳化

此問題已透過新增多個最佳化來解決，以減少在即時/線性資料流中處理DVR視窗所需的時間。

* (ZD #21554) — 未針對以下專案觸發TVSDK錯誤信標： `application-type = video/mp4`

此問題可透過讓播放器對無效資產格式偵測到正確的錯誤追蹤URL來解決。

* (ZD #24424) — 型別的當機 `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` 源自內部 `PSDKLib` 適用於較新硬體裝置上的iOS。

已修正因取消配置媒體播放器例項（在不同串流之間快速切換播放時）而發生的當機問題。

* (ZD #24575) - TVSDK在32位元裝置上當機時 `enableDebugLog=true`

已修正啟用記錄時導致32位元裝置當機的記錄格式問題。

**版本1.4.26** (1.4.26.702) (適用於iOS 6.0+)

* (ZD# 20213) - TVSDK FW必須為XCode7動態/模組化

透過更新支援模組的程式庫來修正

**版本1.4.25** (1.4.25.684) (適用於iOS 6.0+)

* (ZD #19629) — 進入Airplay到ATV 4時直播視訊暫停

此問題可在移除舊專案後但在將新專案新增至之前新增等候期間來解決 `AVQueuePlayer`. 若沒有等候時間，系統會將通知傳送至不正確的專案。

* (ZD #19856) — 預設啟用時不會顯示字幕

已修正webvtt播放清單中造成字幕無法正確顯示的問題。

* (ZD #21590) — 最新原始組建中的視訊效能和追蹤

中缺少視訊長度的問題 `VideoAnalytics` 已修正。

* (ZD #20202) — 設定自訂字幕樣式會讓iOS應用程式當機

此問題已藉由在設定字幕樣式時新增其他null物件檢查來解決。

* (ZD #20709) — 視訊開始追蹤中的視訊長度回報為0

此問題與(ZD #21590)相同。

* (ZD #22280) - Analytics影片長度設為0

此問題與(ZD #21590)相同。

* (ZD #22592) - Primetime中的Airplay問題

此問題與(ZD #19629)相同。

* (ZD#22922) - iOS適用的手動位元速率切換

此問題已透過提供指定最大位元速率的選項而解決。

* (ZD #23084) — 僅IPv6網路符合Apple規範

移除了Apple不建議用於IPv6相容性的符號。

**版本1.4.24** (1.4.24.661) (適用於iOS 6.0+)

* ZD #2548) - Primetime支援行動裝置上的互動式廣告 — VPAID 2.0

如果VPAID廣告無法播放，將邏輯更新為取消隱藏播放器檢視，即可解決此問題。

* (ZD #20101) — 自訂章節實施在廣告播放期間觸發章節開始事件

此問題已透過更新解決 `VideoAnalyticsTracker` 以便在章節與非章節邊界之間轉換時，正確偵測章節開始/完成。

* (ZD #20784) - Analytics：觸發即時視訊轉換的內容完成

此問題已透過新增邏輯來解決，以在視訊追蹤工作階段期間手動觸發內容的完成。

下列程式庫已更新：

* AdobeMobile資料庫至4.10.0
* VHL資料庫至1.5.6
* VHL-Nielsen資料庫至1.6.7
* (ZD #21855) — 中段後不播放字幕

在此問題中，重複的不連續性標籤導致字幕未出現在中段之後。 此問題已透過移除彼此相鄰的不連續標籤來解決。

* (ZD #21994) — 字串超出範圍 `PTHLSUtils`

當機最可能的原因是EXT-X-KEY的URL被引號包圍。

* ZD #22074) - `AUDVAST` 在iOS上每分鐘發生一次當機

在1.4.23版中，已修正VAST重新導向URL中存在不安全字元所導致的當機。 不過，TVSDK會繼續略過這些廣告。

此問題已透過處理不安全字元和允許廣告播放而解決。

* (#22694澤東元) - `PTMediaPlayer`.  檢視已被播放器隱藏

如果VPAID廣告無法播放，將邏輯更新為取消隱藏播放器檢視，即可解決此問題。

**版本1.4.23** (1.4.23.641) (適用於iOS 6.0+)

* (ZD #18016) - Primetime SDK沒有回應且網路狀況不良

改善發生嚴重錯誤時的錯誤通知，即可解決此問題 `AVFoundation` 「 」會發生，且允許應用程式處理錯誤後的重新啟動。

* (ZD #20580) — 當機 `PTSplicerManager`

此問題已透過提供額外保護來避免導致當機的並行問題而解決。

* (ZD #21782) - iOS錯誤碼10100

已修正TVSDK在Adobe存取DRM資料流上開始播放時傳回101000錯誤的問題。

* (ZD #21889) — 線上廣告和離線內容播放失敗

修正AES加密離線內容上的廣告後播放失敗的問題。

* (ZD #22074) - AUDVAST當機在iOS上每分鐘發生一次

改善處理URL中有無效字元的第三方VAST廣告標籤，即可解決此問題。

* (ZD #22257) - TVSDK無法播放DRM資料流

已修正在Adobe存取DRM資料流上開始播放時TVSDK傳回101000錯誤的問題。

**版本1.4.22** (1.4.22.627) (適用於iOS 6.0+)

* (ZD #18709) - iOS的TVSDK當機

已修正某些Adobe存取DRM保護的資料流發生當機的問題。

* (ZD #18850) — 根據CRS規則更新創意選擇邏輯

此問題已透過新增.json設定檔案來指定創意選擇優先順序而解決。

* (ZD #19770) — 受保護的AES視訊摘要不再播放

已修正某些302重新導向資料流無法播放的問題。

* (ZD #19629) — 進入Airplay到ATV 4時直播視訊暫停

在Apple TV 4裝置上開啟Airplay功能後，新增即時視訊暫停的因應措施，即可解決此問題。 問題似乎是Apple TV 4問題。

* (ZD #21119) - TVSDK在廣告播放後停滯

新增支援，可在使用廣告插入時使用序列IV的AES加密資料流。

* (ZD #21125) — 從即時/線性廣告插播回訪

已新增支援，可讓您在廣告插播播放至完成之前從廣告插播回訪。 透過自訂資訊清單標籤指示提早傳回。

* (ZD #21224) - Akamai語匯流的Airplay支援

API已新增至 `PTNetworkConfiguration` 類別來附加Cookie，作為特定Akamai標籤化串流之區段的URL引數。

* (ZD #21287) — 無關記錄

已修正某些記錄陳述式的問題，即使停用記錄時，這些問題也會預設顯示在xcode主控台中。

* (ZD #21446) - TVSDK有時不會觸發廣告插播事件

在「事件」串流上，無法正確觸發先前版本組建中的廣告插播。 此組建解決此問題。

**1.4.21版** (1.4.21.605) (適用於iOS 6.0+)

* (ZD #20749) — 遞補內容略過非空白的VAST回應；引發額外的廣告追蹤URL

後援廣告重複Ping的問題已解決。

**1.4.20版** (1.4.20.590) (適用於iOS 6.0+)

* (ZD #18639) - TVSDK耗費過多的CPU/資源處理冗長的熱錄資產

已在兩個層級中修正過度CPU/資源使用量。 首先，讓時間更新函式在全域佇列上執行，而不是在主執行緒上執行，以及最佳化CPU使用率，以使用先前處理和快取的m3u8剖析資訊清單。

* (ZD #19349) — 節流網路連線時，會略過前段廣告。

此問題已藉由為應用程式和提供逾時事件(requestTimeout)而解決。 `adMetadata.adRequestTimeout` 用於覆寫預設10秒逾時的API。

* (ZD #19446) — 即時資料流上缺少通知

此問題可透過允許應用程式訂閱 `EXT-X-PROGRAM-DATE-TIME` 在即時資料流上。

* (ZD #19459) — 準備替代音訊時當機 `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) — 當機 —  `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此問題與Zendesk #19459相同。

* (ZD #19574) - TVSDK不會傳回DRM或非DRM內容的M3U8回應資料

在中的資訊清單檔案初始載入中 `PTMediaPlayerItem.prepareToPlay`，如果載入資訊清單失敗，TVSDK不會向應用程式回報失敗回應的內文。

允許TVSDK將失敗回應回報給應用程式，即可解決此問題。

* (ZD #19615) — 遞補邏輯無法運作

在目前的實作中，已略過遞補廣告，除非這些廣告為m3u8格式，否則不會重新封裝。 此問題已透過新增重新封裝遞補廣告的支援而解決。

* (ZD #19770) - TVSDK無法使用302重新導向播放任何受保護的AES內容

已修正重新導向問題，因為重新導向URL已被清除 `cleanConnectionData` 才能用於剖析資訊清單。

* (ZD #19856) — 預設啟用時，某些位元速率不會顯示字幕

此問題已透過處理iOS針對未顯示字幕的資料流區段所傳回的錯誤而解決。

* (ZD #19868) - TVSDK在販運無效創意時當機

已修正TVSDK中錯誤取消配置Vast剖析器執行個體的當機問題。

* (ZD #20180) — 偶爾會略過VPAID廣告

JavaScript MIME型別並非總是包含或視為有效的MIME型別。 將JavaScript加入為有效的MIME型別，即可解決此問題。

* (ZD #20749) — 遞補內容略過非空白的VAST回應；引發額外的廣告追蹤URL

已修正部分創意內容未重新封裝的問題。

**版本1.4.19** (1.4.19.563) (適用於iOS 6.0+)

* ZD #18639) - TVSDK在冗長的熱錄影資產上佔用過多的CPU/資源

此問題已透過最佳化DRM m3u8播放清單重寫至播放清單中先前已重寫的快取位元來解決。 當您播放即時m3u8資料流（每次下載區段後都會下載該資料流的m3u8）時，此資料流最相關。

* (ZD#18956) - `player.drmManager` 在iOS示範播放器中設定中斷點時，為nil

此問題已透過更新 `PTMediaPlayer.drmManager` 從DRM架構擷取DRMmanager的API實作。

**版本1.4.18** 適用於iOS 6.0+的( 1.4.18.557)

* (ZD #18844)在iOS播放器中追蹤即時內容的播放點。

允許應用程式設定自己的播放點值，即可解決此問題。

* (Zendesk #18518) — 如果未指定視訊名稱，TVSDK的名稱會預設為*以PSDK為基礎的播放器。*

此問題已透過移除播放器名稱的預設值來解決。

**版本1.4.17** (1.4.17.545) (適用於iOS 6.0+)

* (Zendesk #2228) — 增強TVSDK以傳回擷取資訊清單的JSON回應

DRM Framework不會在內容不是M3U8時傳送錯誤，而是傳回nil DRMMetadata。 透過新增中繼資料以在M3U8_PARSER_ERROR通知發生時公開內容，該問題已得到解決。

* (Zendesk #2231) — 擷取MediaPlayerNotification中無法使用的資訊清單時傳回錯誤

與Zendesk #2228相同的解析度

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` 未填入巨集

以下問題： [!DNL Auditude] 當追蹤URL的開頭有空格的問題解決後，SDK無法傳送Ping。

* (Zendesk #17294) — 當機 [!DNL SecKeyRawSign]

已解決客戶的程式碼使用金鑰鏈結時可能發生的當機問題。

* (Zendesk #18008) — 支援iOS8+的Cookie以支援代碼化的資料流

Akamai代碼化的資料流要求在區段請求時傳送Cookie，但在iOS 7和更早版本上無法做到這一點。 從iOS 8開始，Apple已新增API允許為區段請求傳遞Cookie。 TVSDK現已提供這項支援。 已新增傳送使用者代理程式（若有）的支援。

* (Zendesk #18166) - TVSDK 1.4.15在使用編譯時會發出數百個警告 `DWARF` 替換為 `dSYM` 檔案選項

所有警告已解決。

**注意**：已為TVSDK新增tvOS相容程式庫。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 — 播放期間Tab S當機

回覆OKHTTP對的相依性 [!DNL Auditude] 對於CRS，因為TVSDK現在直接使用 `httpurlconnection` 而不是curl。 此問題已透過在發出另一個JNI呼叫之前清除例外來解決。

* (Zendesk #4487) — 追蹤線性內容頻道

線上性資料流播放工作階段期間，透過重新初始化視訊心率追蹤器來解決問題。

* (Zendesk #17919) - Android — 內容搜尋導致心率錯誤

問題是當章節中有搜尋時，解決錯誤狀態的心率

* (Zendesk #18053) — 使用TVSDK的應用程式會在棉花糖上當機

TVSDK程式庫使用YUV的Neon程式碼時，TVSDK在Android™ M作業系統上當機 `->` RGB色彩轉換。 此問題已透過使用非Neon版本的 `code`.

* (Zendesk #18072) - Android M — 應用程式當機

此當機發生在呼叫時 `MediaCodecList` 和 `MediaCodecInfo` 檢查是否支援設定檔和層級時的API。 Adobe正在尋求Google對額外深入分析的支援。 此問題已透過提前載入所有轉碼器資訊來提供暫時因應措施，以避免僅在需要轉碼器資訊時呼叫這些API，進而解決。

* (Zendesk #18074) - Nexus搭配Android™ 6.0無法使用的阿拉伯文字幕

此問題已藉由支援Android™ CTS字型對應而解決。

**版本1.4.15** (1.4.15.512) (適用於iOS 6.0+)

**注意**： Nielsen模組已從TVSDK建置版本中移除，但TVSDK將很快更新為新的Nielsen整合模組。

* (ZD #2228) — 擷取資訊清單傳回的錯誤，無法在 `MediaPlayerNotification`

新增中繼資料，以在通知時公開內容 `M3U8_PARSER_ERROR` 發生。

* (ZD #4437) - Adobe Primetime SDK內的當機

修正準備字幕/替代音訊時報告的當機問題。

* (ZD #4487) — 追蹤線性內容頻道

允許線上性資料流播放工作階段期間重新初始化視訊心率追蹤器。

**版本1.4.14** (1.4.14.498) (適用於iOS 6.0+)

* (ZD #17260) — 當機於 `playlistManagerForURL`

修正了因並行問題造成的間歇性當機。

**版本1.4.13** (iOS 6.0+)

* (#3304元) - VAST 3.0 `[ERRORCODE]` 未填入巨集

   * 如果內嵌廣告具有不良創意，則會顯示錯誤代碼400。
   * `[ERRORCODE]` 巨集已進行URL編碼。

* (ZD #3865)心率與IMA廣告整合

修正錯誤回報視訊長度的問題。

* 更新TVSDK示範播放器以支援iOS 9

若要正確支援iOS 9，您必須設定Application Transportation Security的例外狀況。 在示範中，ATS會完全停用。

**版本1.4.12** (1.4.12.464) (適用於iOS 6.0+)

* (ZD #4521) CRS測試使用者端和SSAI

修正3P URL中錯誤的反向MD5。

**版本1.4.12** (1.4.12.463) (適用於iOS 6.0+)

* (ZD #2751) CSAI和CRS /增強：處理特定媒體檔案URL中的動態元素。

更新Creative重新封裝服務，以正確處理具有動態創意URL的廣告。

* (ZD #3654) 1.3.4.166版之後的PSDK版本發生記憶體流失

修正中的記憶體流失 `drmFramework` 在iOS 8.2裝置上定期播放

* (ZD #3988)第一次播放後重新搜尋時會略過Preroll

修正錯誤，以便正確停用廣告原則。

* (ZD #4017)請求iOS API強制向後搜尋播放廣告

已解決ZD#4279案的修正

* (ZD #4279) iOS和桌上型電腦上的HLS TVSDK廣告插入–302重新導向問題

修正廣告資產使用相對重新導向URL時的錯誤

**版本1.4.9** (1.4.9.427) (適用於iOS 6.0+)

* (ZD #3075)網際網路連線能力問題 — iOS

已新增通知，以偵測播放何時停止。

* (ZD #3193) TVSDK中的設定檔變更API要求

已更新 `PTPlaybackInformation` 以公開更新的指定位元速率。 已更新 `BITRATE_CHANGE` 通知，可更可靠且精確到M3U8報告的位元速率。

* (ZD #3324)當VMAP中沒有廣告媒體時，Primetime廣告報告問題

支援釘選空白廣告插播追蹤URL，TVSDK現在會驗證空白廣告插播的廣告插播開始和完整Ping。

**版本1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7在完整事件重播中當機

**版本1.4.7** (1.4.7.382)

* (ZD #2197)追蹤廣告錯誤。 為無法載入資訊清單的資產新增通知。
* (ZD #2894)播放器在播放期間提出四個頂層資訊清單請求。
* (#2992斐濟元) [!DNL Auditude] 報告奇怪的持續時間和識別碼。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)追蹤廣告錯誤。 已新增資產無法載入資訊清單的通知

**版本1.4.5** (1.4.5.283)

* (ZD #2141) Analytics實作，適用於 [!DNL TreeHouse] 應用程式，已新增 `AdobeAnalyticsPlugin.a` 程式庫以建置套件。
* 視訊心率資料庫更新至1.4.1.2
* (PTPALY-4226) (與ZD #2423相關)執行DRM重設會導致刪除應用程式檔案資料。

**版本1.4.4** (1.4.4.242)

* 視訊心率程式庫(VHL)更新至1.4.1。

* (ZD #2435)分析需求更新的TV SDK檔案

**版本1.4.2** (1.4.2.210 ： iOS 6.0+)

* (#1129斐濟元) `_player.currentItem.audioOptions` 傳回空白
* (ZD #2109) Primetime PSDK 1.4.1.125無法搭配Xcode 5.1.1運作
* (ZD #2137)無法載入DRM中繼資料時，iOS上的PSDK當機

**版本1.4.1**(1.4.1.125)

* (#1107斐濟元) [!DNL CocoaLumberjack] 複製符號
* (ZD #1644)修改用於鎖定目標和報告的iOS使用者代理
* (ZD #1850) iOS SDK中包含的Cocoa Lumberjack檔案
* (ZD#1908)如果超過1個，PSDK會忽略自訂標籤

**1.4.0版** (1.4.0.32)

* Zendesk #1024 — 透過資訊清單從資料流中移除廣告的功能

## 裝置認證與支援 {#device-certification-and-support}

>[!NOTE]
>
>下列功能為 **not** TVSDK支援：
>
>* 在任何平台或版本上，動作緩慢。
>* 即時特技播放。


**版本1.4.43**

* TVSDK 1.4.43已通過iOS 11的認證。

**版本1.4.29**

* TVSDK 1.4.29已通過iOS 10的認證。

**版本1.4.28**

* TVSDK 1.4.28已通過iOS 10 Beta 7的認證。
* DRM支援透過新增強制HTTPS  `forceHTTPS`  和 `isForcingHTTPS` API。
* 將VHL程式庫更新至1.5.8、將Mobile程式庫Adobe至4.8.4，並將記錄器公用程式程式庫更新至7.0版部署目標。

**版本1.4.19**

此版本的TVSDK已通過iOS和tvOS的FairPlay支援認證。

**版本1.4.17**

* tvOS

   此版本的TVSDK支援tvOS，並經過未加密的HLS資料流認證。

   **注意**：請記住以下編譯准則：

   * TVSDK tvOs支援僅限於非Adobe的DRM加密資料流。 您必須移除參照 `drmNativeInterface.framework` 在您的tvOS組建設定中。 仍支援AES加密資料流。
   * Apple要求所有Apple TV應用程式都必須啟用位元代碼，因此您必須在專案設定中開啟此標幟。

## 已知問題和限制 {#known-issues-and-limitations}

* 由於iOS UIWebView類別已過時，在iOS TVSDK 3.6以後：
   * VPAID廣告在iPad 13中無法如預期播放。
   * 隨附廣告無法如預期播放。

* 在iOS TVSDK中，所有廣告都會連結至內容資訊清單。 廣告行為是透過根據內容和廣告區段的持續時間進行搜尋來實作。 因此，如果區段持續期間不準確，搜尋可能不會一律在廣告插播開始或結束的確切影格結束。 即使持續期間在框架上，平台本身也會在搜尋上施加容許度，而且可能會顯示一些框架、廣告或內容。 這是平台的限制，以及廣告插入在iOS上搭配TVSDK使用的方式。
* 在此情況下，跳過的決定會發生在搜尋事件上。 不過，由於資訊清單中的廣告區段持續時間無法準確表示廣告的實際持續時間，因此搜尋的框架不正確。 因此，您會在套用廣告原則時看到一些廣告畫面。
* 它可能會體驗到授權輪換影片無法在iOS 11上播放，且在iOS 9.x和iOS 10.x上播放時可能會沒有問題。
* 在VPAID 2.0支援中，如果透過AirPlay有效播放，則會略過VPAID廣告。
* 此 `drmNativeInterface.framework` 當最小目標設定為iOS7 （或更新版本）時，無法正確連結。
因應措施：明確指定 `libstdc++.6.dylib` 程式庫，如下所示：前往 **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** 並新增 `libstdc++.6.dylib`.
* 未插入取代API的後置式廣告。
* 在廣告插播中搜尋（不退出）會發佈重複的廣告開始和廣告插播通知
* 設定 `currentTimeUpdateInterval` 沒有任何效果。
注意：在某些iOS版本中，作業系統不會載入內的資源 `PSDKLibrary.framework` 自動。 請務必手動複製 `PSDKResources.bundle` 至應用程式的套件資源：前往 **建置階段** 和複製套件組合資源。
* 無法使用Xcode 8或更低版本建置參考應用程式。 iOS TVSDK 1.4.41版以後，請使用Xcode 9進行編譯。
* VPAID廣告不遵守 `delayAdLoadingTolerance` 值。
* 24077 — 對於某些具有字幕的HLS內容，播放器當機於 _停止_ 或 _重設_ 方法。
* 啟用「即時」廣告解析時，無法使用詳細的錯誤通知。
* 錯誤通知會根據廣告解析時間記錄，而非根據廣告序列記錄。
* 此版本中的HEVC支援有下列限制
   * 不支援DRM
   * CC (CEA 608/708)支援無法使用，因為CMAF不支援。
   * 尚未提供4K支援。
   * ID3標籤不支援，因為它在CMAF中不受支援。
   * 未驗證未停用的即時HEVC資料流。
   * 未驗證HEVC Ads支援。
* 啟用JIT且容許度設為10秒時，如果有VMAP > VAST重新導向廣告，則第一個中繼廣告插播不會看到VAST呼叫。
* 為了讓廣告解析度逾時正常運作，播放器預計在即時資料流播放期間每次更新播放清單時，會在20秒內產生拼接的播放清單。 若未在上述間隔內收到拼接的播放清單，則會擲回內部錯誤，且播放器會停止。

## 實用資源 {#helpful-resources}

* [適用於iOS程式設計師的TVSDK 3.4指南](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDK iOS 3.4 API參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://experienceleague.adobe.com/docs/primetime.html) 頁面。
