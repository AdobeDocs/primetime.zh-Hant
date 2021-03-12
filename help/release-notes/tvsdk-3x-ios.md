---
title: iOS版TVSDK 3.13發行說明
description: iOS版本注意事項的TVSDK 3.13說明TVSDK iOS 3.13中有哪些新增或變更、已解決和已知問題以及裝置問題。
translation-type: tm+mt
source-git-commit: d1cf8a05172c04655c8a7c76ce116c8f7be61ec9
workflow-type: tm+mt
source-wordcount: '7713'
ht-degree: 0%

---


# iOS版TVSDK 3.13發行說明{#tvsdk-for-ios-release-notes}

iOS版本注意事項的TVSDK 3.12說明TVSDK iOS 3.12中有哪些新增或變更、已解決和已知問題以及裝置問題。

## 系統和軟體要求{#system-software-requirements}

在下載iOS 3.12之前，請確定您的硬體、作業系統和應用程式版本符合下列需求：

作業系統：iOS 8.0或更新版本。

## iOS TVSDK 3.13

本版次針對即時、VOD和FER串流提供DEMUXED &#39;HLS/CMAF&#39;（前滾、移轉和後滾）廣告支援。

有關客戶報告問題的修正，請參閱[已解決問題](#resolved-issues)。 有關限制，請參見[已知問題和限制](#known-issues-and-limitations)。

### 舊版{#whats-new-previous}中的新功能和修正

**iOS TVSDK 3.12**

已修正即時串流在播放15分鐘後失敗的問題。

**iOS TVSDK 3.11**

針對`isFallbackOnInvalidCreativeEnabled`和方法`customParams`導致應用程式當機的客戶問題提供修正。

**iOS TVSDK 3.10**

* 修正當網路無法使用時，TVSDK播放器無法觸發`PTMediaPlayerStatusError`通知的問題。

**iOS TVSDK 3.9**

* 修正VTT字幕無法播放導致應用程式凍結的問題。

* iOS TVSDK 3.9包含更新的個人化傳輸憑證。

**iOS TVSDK 3.8.0.83 Hotfix**

修補程式具有更新的個人化傳輸憑證。

**iOS TVSDK 3.8**

iOS 13合規性並處理iOS 13 UIWebView API取代問題。

**iOS TVSDK 3.7**

同時提出大量廣告解析度要求時，播放停止的藍本的修補程式。

**iOS TVSDK 3.6**

**修正類別中廣泛的XML屬性`PTNetworkAdInfo`**

wastXML屬性未正確設定，傳回nil值。

**iOS TVSDK 3.5**

**啟用背景音訊**

*設定您的應用程式，以便在進入背景時繼續播放音訊。*

若要啟用此功能，我們必須設定PTMediaPlayer類別中新增的新API `audioPlaybackInBackground`。 啟用此API後，您的應用程式就可以播放背景音訊。

**iOS TVSDK 3.4.0.19（修補程式）**

此版本已修正廣告容錯案例中發生的應用程式當機問題。

**iOS TVSDK 3.4**

**廣告解析度逾時**

* 使用TVSDK 3.4，使用者現在可以設定整體廣告解析度和資訊清單下載的逾時值。 如果在指定的逾時內，有些廣告不會    已解決，TVSDK將播放剩餘的廣告。

* PTAdMetadata:adRequestTimeout API已過時，將會移除。 預設值已設為35秒。

* PTAdMetadataClass中引入了兩個新的替代API:adResolutionTimeout —— 整體廣告解析度呼叫的逾時                adManifestTimeout —— 廣告資訊清單下載的逾時。

**收入最佳化**

啟用TVSDK來識別與廣告插入工作流程相關的問題區域，以向分析的選擇終點報告。

**第3.3版**

TVSDK 3.3現在符合iOS 11 SDK的規範。 所有已過時的API都已取代為適當的替代項目。

**第3.2版**

**其他記錄支援（階段2）**

新增錯誤通知的支援，以防發生下列情況：

* HLS版廣告使用的層級高於內容。

* 排除純音訊變型。

* VAST/VMAP請求失敗。

**第3.1版**

* **其他記錄**
支援新增在廣告播放失敗時對說明性通知的支援。

* **新增Fairplay加密的CMAF串流支**
援Fairplay Encrypted的CMAF串流與AVC codec播放現在受支援。

**3.0.1版**

此發行中沒有新功能或增強功能。

**3.0版**

* TVSDK 3.0支援HEVC串流。

* 及時解決——解析更接近廣告標籤的廣告。

新增「應用程式層級」介面上布林類型的`enableDelayAdLoading`屬性，以啟用JIT。 如果`enableDelayAdLoading`為NO，則`setadMetadata.delayAdLoading`將轉換為True（PTAdMetadata介面的屬性）。

啟用此屬性後，TVSDK會根據定義的容差值，先解決每個廣告插播。 根據預設，`delayAdTolerance`設定為5秒。

**1.4.45版**

為符合Xcode10,TVSDK已從「`libstdc++`」移至「`libc++`」，因此支援的最低版本為iOS 7。 之前是iOS 6。

**1.4.44版**

此發行中沒有新功能或增強功能。

**1.4.43版**

* 類似電視的體驗，讓您能夠在廣告中間加入，而不觸發部分廣告追蹤。\
   範例：使用者在90秒廣告插播（包含3個30秒廣告）的中間（40秒）加入。 這是分段內第二個廣告的10秒。

   * 第二個廣告會在剩餘期間（20秒）播放，接著是第三個廣告。
   * 不會觸發已播放之部分廣告（第二個廣告）的廣告追蹤器。 只會觸發第三個廣告的追蹤器。

* 在PTAdMetadata介面中新增布林類型的enableVodPreroll屬性。 該屬性可用於啟用VoD串流的前滾。 如果enableVodPreroll為NO,PSDK不會播放前置播放。 然而，這並不會對微軟造成影響。 enableVodPreroll的預設值為YES。
* PTMediaPlayer介面的closedCaptionDisplayEnabled API從iOS v1.4.43開始標示為不建議使用。 若要判斷特定PTMediaPlayerItem是否有隱藏字幕，請檢查PTMediaPlayerMediaItem的subtitlesOptions屬性。

**1.4.42版**

此版本未新增任何新功能。 有關已修復的問題清單，請參見[已解決的問題](#resolved-issues)。

**1.4.41版**

API變更：

* **isSecure**:推出新的isSecure API，以保護播放器不會錄制和擲出錯誤。預設值為true。

* **allowExternalRecording**:引入新的API，允許對安全內容進行空中鏡像。Airplay鏡像視為記錄，因此`allowExternalRecording`值必須設定為`True` ，以允許airplay鏡像或設定為`False` ，以停止airplay鏡像以保護內容。 依預設，`value`為true。

**1.4.40版**

無新功能。

**1.4.39版**

* iOS TVSDK已取得VHL 2.0.1認證，而VHL 2.0.1已取得Nielsen認證。

* iOS TVSDK已更新，以從新的Akamai主機`primetime-a.akamaihd.net`發出CRS請求。

* 新的主機名稱設定提供CRS資產傳送，可透過HTTP和HTTPS(SSL)進行更大規模的傳送。

**1.4.36版**

在iOS TVSDK中整合及認證VHL 2.0:透過降低API的複雜性，降低`VideoHeartbeatsLibrary`實作中的障礙。

**1.4.34版**

**網路廣告資訊**

TVSDK API現在提供協力廠商VAST回應的其他資訊。 廣告ID、廣告系統和廣告延伸模組提供於`PTNetworkAdInfo`類別中，可透過廣告資產的`networkAdInfo`屬性存取。 此資訊可用於與其他廣告分析平台整合，例如&#x200B;**Moat Analytics**。

**1.4.31版**

* **帳單** 量度Adobe會收集使用量度，並使用這些量度來決定向客戶收取多少費用，以容納只想支付其使用費用的客戶，而非不考慮實際使用的固定費率。

   每當TVSDK產生串流開始事件時，播放器就會定期傳送HTTP訊息至Adobe的帳單系統。 標準VOD、專業VOD（啟用中間卷廣告）和即時內容的時段（稱為計費持續時間）可能不同。 每種內容類型的預設持續時間為30分鐘，但您的Adobe合約會決定實際值。

* **CRS** AdsTVSDK的多CDN支援現在支援CRS廣告的多CDN。透過提供CRS廣告的FTP詳細資訊，您可以指定CDN位置，而非預設Adobe擁有的CDN（例如Akamai）。

**1.4.29版**

在`PTSDKConfig`類別中，已新增forceHTTPS API。

`PTSDKConfig`類別提供對向Adobe Primetime廣告決策、DRM和視訊分析伺服器提出的要求強制執行SSL的方法。 如需詳細資訊，請參閱此類別的`forceHTTPS`和`isForcingHTTPS`方法。 如果透過HTTPS載入資訊清單，TVSDK會保留HTTPS的內容使用，並在從資訊清單載入任何相關URL時會尊重此使用方式。

>[!NOTE]
>
>對第三方網域（例如廣告追蹤像素、內容和廣告URL）的請求以及類似的請求不會修改，內容提供者和廣告伺服器有責任提供透過HTTPS支援的URL。

**1.4.18版**

Primetime iOS TVSDK現在支援VPAID 2.0 Javascript創意素材，以提供豐富的互動串流內廣告體驗。 如需VPAID 2.0的詳細資訊，請參閱VPAID廣告支援。

**1.4.17版**

* tvOS

   TVSDK支援tvOS原生應用程式。
* 可播放下列類型的內容：

   * VOD
   * 即時
   * AES-128
   * 替代音訊和字幕
   * FER

* 可顯示下列類型的廣告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 目前不支援下列功能：

   * Digital Rights Management(DRM)
   * 廣告橫幅
   * 電視標籤語言(TVML)

**1.4.13版**

>[!NOTE]
>
>Nielsen模組已從TVSDK組建版本移除，TVSDK將於近期內更新，並新增Nielsen整合模組。

**廣告備援，廣告選擇邏輯中的菊花鏈(Zendesk #3103)**

對於啟用備援規則的VAST廣告（創意人員）,TVSDK會將無效MIME類型的廣告視為空白廣告，並嘗試使用備援廣告。 您可以設定備援行為的某些方面。 如需詳細資訊，請參閱VAST和VMAP廣告的廣告後援。

**1.4.9版**

**具有替代內容替換的封鎖信號**

在1.4 TVSDK更新中，我們現在也支援針對線性內容進行區域封鎖並重新啟用。 TVSDK現在可以並行處理主要和替代的兩個資訊清單檔案，以便監控封鎖訊號，即使替代原始程式設計顯示替代程式設計。

**1.4.8版**

**視訊心率程式庫(VHL)已更新至1.5版**

* 能夠以視訊開始和／或視訊／廣告／章節開始傳送中繼資料作為內容資料。

* 網路流量減少——心率平均會減少，而且會變小。

**1.4.7版**

* **現場個人化支援**

支援Adobe個性化伺服器的現場安裝，以定制客戶端的個性化請求，以轉到不同的端點。

* **基於解析度的輸出保護**

DRM策略現在可以根據設備的輸出保護功能指定允許的最高解析度。 例如，「如果有HDCP，則允許播放高達1080p解析度的內容，如果沒有HDCP，則允許播放高達480p解析度的內容」。

**1.4.4版**

* **視訊心率程式庫(VHL)更新至1.4.1.1版**

   * 新增搭配Adobe Analytics視訊基本工具，搭售其他SDK或播放器的不同分析使用案例的能力。
   * 已移除`trackAdBreakStart`和`trackAdBreakComplete`方法，以最佳化廣告追蹤。 廣告插播是從`trackAdStart`和`trackAdComplete`方法呼叫推斷而得。
   * 追蹤廣告時，不再需要`playhead`屬性。
   * 新增對Marketing Cloud訪客ID的支援。

* **Nielsen SDK整合**

TVSDK現在支援傳送mTVR和MDPR ID3信標至Nielsen SDK，毋需任何自訂整合。 若要開始使用，請下載3.1.2.19 Nielsen iOS App SDK，然後依照iOS Programmers Guide中的說明進行。

**1.4.0版**

* **具有替代內容替換的封鎖信號**

在1.4 TVSDK更新中，TVSDK現在也支援針對線性內容進行區域封鎖後進入和返回。 TVSDK現在可以並行處理主要和替代的兩個資訊清單檔案，以便監控封鎖訊號，即使替代原始程式設計顯示替代程式設計。

* **移除／取代C3廣告**

現在，您不需要額外的準備工作，就能將新廣告動態插入從C3視窗傳出的隨選視訊(VOD)資產。 TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 此強大的新功能在廣播期間播放即時／線性內容時也很有用，而且會立即下拉以做為隨選內容，而無需適當的時間來「清理」資產。

## 已解決問題{#resolved-issues}

如果解析度與報告的問題相關聯，則會顯示Zendesk參考，例如ZD#xxxxx。

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

* (ZD 42085)-在CMAF串流上播放的問題。

* (ZD-43215)-在廣告進行中時關閉播放器時當機。

* (ZD 43210)-啟用WebVTT字幕時，iOS HLS回放將凍結。

**iOS TVSDK 3.12**

* 使用iOS 3.10版的TVSDK時，在播放15分鐘後即時串流會失敗。

### 已解決舊版{#resolved-issues-previous}中的問題

**iOS TVSDK 3.11**

* (ZD#40998)- `isFallbackOnInvalidCreativeEnabled`會導致應用程式當機。

* (ZD#41289)-使用`customParams`方法觀察到`NSInvalidArgumentException`導致應用程式當機。

**iOS TVSDK 3.10**

(ZD#40943)-當網路不可用時，TVSDK播放器不會觸發PTMediaPlayerStatusError通知。

**iOS TVSDK 3.9**

(ZD#40272)- iOS TVSDK無法播放VTT字幕，並出現101001錯誤，導致應用程式凍結。

**iOS TVSDK 3.8**

* (ZD#40087)- iOS當機，且播放器錯誤導致過期的VOD內容。

* (ZD#40083)- Pre-Roll廣告不會針對具有`OpportunityGenerator`的即時串流播放，而播放器會出現錯誤。

* (ZD#39828)- `CurrentItem`屬性遺失nullability註解，當通知中包含的播放器狀態為`PTMediaPlayerStatusStopped`時，會造成播放器當機。

**iOS TVSDK 3.7**

(ZD#38961)-當多個內容設定為在PiP中播放時，當一個內容完成播放後，內容無法在「畫中畫」(PiP)視窗中播放。

**iOS TVSDK 3.6**

此發行中沒有新問題。

**iOS TVSDK 3.5**

此發行中沒有新問題。

**第3.3版**

(ZD#37820)-新增自訂標題HS-Id、HS-SSAI-TAG的允許清單。

**第3.2版**

* **Ticket#36588** -呼叫MediaPlayer STOP方法時，會觀察到播放器損毀。

已修正呼叫STOP方法以取得少數具有字幕的串流時，所觀察到的間歇性損毀。

* **Ticket#37080** - Manifest呼叫的重複請求。已修正播放期間對資訊清單URL重複提出的要求。 TVSDK現在會針對每份資訊清單發出一個呼叫。

* **Ticket#37** - CRS標準化規則失敗，並包含eq符合類型修正播放器在與具有&quot;eq&quot;符合類型之主機名稱的上次標準化規則集碰撞時，會當機的案例。

**第3.1版**

**票證#36313** -線性廣告中斷期間的間歇性不可預測結果在即時串流中的線性廣告中斷期間，固定間歇性播放。

**3.0.1版**

**Ticket36948** - CRS - iOS 12上不一致的資產選擇順序為CRS選擇的資產並不總是在VAST或VMAP響應中返回的最高質量變數。

**3.0版**

* **Ticket35311** -在電話呼叫中斷期間，播放器狀態不會變為「暫停」新增中斷處理常式，以阻止播放器中斷。當中斷時，播放器狀態會變為「暫停」，然後按一下播放按鈕繼續播放。

* **Ticket36685** -即時資產——與播放器時間進度和SCTE標籤時間不符的時間會針對即時點前方的SCTE標籤計算正確時間。

* **Ticket36492** - `currentTime`  `localTime` 且在暫停狀態期間尋找新位置時未更新，現在，當播放器處於暫停狀態時，播放器的目前時間可設為零；稍早的目前時間，會設為僅在播放狀態中為零。

**1.4.45版**

* **Ticket36294** - iOS TVSDK無法與Xcode 10搭配運作已修正XCode 10上TVSDK的編譯問題。由於XCode 10的需求，iOS 1.4.45版以上的TVSDK為基礎建立的應用程式需要最低部署目標，如iOS 7.0

* **Ticket36321** -在「播放」狀態中，在 `PTMediaPlayer` 與 `AVPlayer` 例項之間可查看的範圍中觀察到的差異。

* **Ticket36493** -  `libstdc++` iOS 12的支援已修正iOS 12上TVSDK的編譯問題。以iOS 1.4.45版之前的TVSDK為基礎建立的應用程式，在iOS 7.0版之前，需要最低部署目標

**1.4.44版**

* **Ticket34683** -廣告播放進度時間為負

當廣告伺服器所報告的持續時間與實際廣告內容不符時，會進行其他檢查以處理此情況。

* **Ticket34801** - currentTime和localTime在暫停狀態期間搜尋新位置時未更新，現在播放器處於暫停狀態時，可將播放器的目前時間設定為零；稍早的目前時間，會設為僅在播放狀態中為零。

* **Ticket35037**  —— 從訊號式廣告插入返回時，播放會停止有錯誤的URL。已改善1.4.42版本中已關閉問題#34385的修正。 已新增isCancelled檢查和異常處理代碼，讓作業佇列更為健全。

**1.4.43版**

* (ZD#32990)- iOS:在某些提示點上播放內容，而非播放廣告。 `selectedMediaOptionInMediaSelectionGroup` 屬於AVPlayerItem介面的API現在已移至iOS 11的AVMediaSelection下。此新API已解決此問題。

* (ZD#33683)從中繼資料字串移除的TVSDK ==字尾。 問題已修正在剖析邏輯中。

* (ZD#33905)- iOS TVSDK使用兩個使用者代理呼叫資訊清單檔案。 已修正第一次m3u8呼叫（新安裝案例）的使用者代理問題。 現在，M3u8的所有呼叫都有相同的使用者代理。

* (ZD#34293)-插入線性串流的預卷無法在iOS11上正確播放。 前置廣告的問題已修正。

* (ZD#34684)-套用廣告略過原則時，前段廣告影格會顯示數秒。 已引入新的API enableVodPreroll，可停用vod播放中的前置播放。 此API的預設值為「是」。 API可確保在主要內容中跳過廣告內容拼接。

* (ZD#34765)-呼叫stop()後，仍有少數傳輸串流區段會下載。 已增強Stop()API，以避免下載額外的區段。

* (ZD#34865)-即時串流的前段廣告會在iOS上截斷。 與iOS11相關，並新增額外的檢查來確認串流是預先播放還是主要內容，以解決此問題。

* (ZD#35093)-修正若串流的主要變數在啟動時失敗（傳回404），則播放不會切換至備份串流的容錯情形。

**1.4.42(1.4.42.118)**

* (ZD#34385)-從訊號式廣告插入返回時，播放會停止有錯誤的URL。

   增加`CustomAVAssetLoaderOperations`的最大併發計數，以便資訊清單讀取繼續執行。

* (ZD#34373)-當不允許串流錄制時，終端用戶無法串流至HDMI連接的裝置。

* (ZD#32678)- TVSDK不會在iOS上收集正確的廣告ID。

   在VHL ping中，如果發生VAST/VMAP重新導向，現在會擷取最終廣告創意素材的廣告ID。

* (ZD#33904)- TVSDK未註冊AVFoundation通知`AVAudioSessionMediaServicesWereLostNotification`和`AVAudioSessionMediaServicesWereResetNotification`。

   `PTMediaServicesWereLostNotification` 現在 `PTMediaServicesWereResetNotification` 可在播放器應用程式中註冊，以在媒體服務重設或遺失時取得通知。

* (ZD#33815)-客戶無須更新應用程式，就無法更新其優先順序和標準化CRS規則。

   將`getCRSRulesJsonURL`和`setCRSRulesJsonURL` API新增至iOS TVSDK。

**1.4.41版(1.4.41.76)**

* (ZD #34464)-使用TVSDK 1.4.41版建立參考應用程式的問題

   從這個版本開始，編譯iOS的TVSDK需要Xcode 9。
* (ZD #29456)-暫停狀態下播放開始

   已修正「影片進入播放時暫停」的暫停問題。
* (ZD #30371)-當我們線上性串流中插入超過2個廣告時，AdBreak開始時間會變更

   已修正嘗試在Apple TV上播放內容時發生的錯誤，此錯誤會完全導致無法播放
* (ZD #32146)-封鎖iOS 11開發測試版時，收到HLS Live內容的`PTMediaPlayerStatusError`

   使用Charles（Drop connection和403）封鎖時，未收到HLS Live和VOD內容的`PTMediaPlayerStatusError`。

* (ZD #29242)- Airplay Video Playback Fails With Ads Enabled.

   當廣告啟用且AirPlay啟用開始播放視訊時，視訊播放不會開始，且不會顯示錯誤。

* (ZD#33341)- `DRMInterface.h`會在Xcode 9中觸發建置警告。

   已修正`DRMInterface.h`中遺失參數清單中「void」字詞的兩個區塊原型。

* (ZD#31979)-當iPhone 7/iPhone7+的iOS 10或更新版本為iOS 10時，不編譯／執行。

   已修正不再支援編譯iOS 7之前的IB檔案。

* (ZD#32920)-廣告插播內的空白畫面，無廣告插播完成。

   當廣告插播呈現廣告例項，且廣告例項完成後，會顯示空白畫面。

* (ZD#32509)-停用iOS 11螢幕錄制在iOS 11上停用螢幕錄制。

* (ZD#33179)- iOS11上的間歇性事件失敗。

   已修正iOS 11上的事件失敗。

**版本1.4.40** (1.4.40.72)

* (ZD #32465)-播放器無法處理合併的播放器清單。

   呼叫`finishLoadingWithError`(使用：錯誤)，以便AV基礎嘗試替代串流／觸發器故障切換。

* (ZD #31951)-授權輪替期間發生TVSDK錯誤。

   已修正授權輪換問題。
* (ZD #31951)-廣告插播內的空白畫面，無廣告插播完成。

   已處理Facebook VPAID廣告通常在單個`<AdParameters>` VAST節點中返回多個CDATA塊的問題。
* (ZD #33336)- iOS TVSDK —— 廣告pods未填入，儘管Freewheel傳回的廣告數量足夠。

   已建立序列廣告與備援廣告之間的父子關係，並根據父序列與索引排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178)- iOS TVSDK版本不正確。

   記錄檔中的TVSDK版本輸出為1.0.211。它已修正為輸出正確版本。

* (ZD #32199)-延遲廣告載入——不會針對內容顯示視訊。

   先前未初始化的本機Adbreak時間軸現在會在使用前重新整理。

* (ZD #27528)-如果iOS 1.2的次要音訊設為非預設值，則資產開始播放後1-45秒內，視訊、音訊或兩者皆凍結。

   以「就緒」狀態準備音軌並通知音軌。

* (ZD #30411)-如果您選擇次要的Sap語言，您可能會收到非預期的結果，例如無音訊或不正確的音訊。

   以「就緒」狀態準備音軌並通知音軌。

* (ZD #32199)-延遲廣告載入——不會針對內容顯示視訊。

   先前未初始化的本機Adbreak時間軸現在會在使用前重新整理。

* (ZD #27528)-如果iOS 1.2的次要音訊設為非預設值，則資產開始播放後1-45秒內，視訊、音訊或兩者皆凍結。

   以「就緒」狀態準備音軌並通知音軌。

* (ZD #30411)-如果您選擇次要的Sap語言，您可能會收到非預期的結果，例如無音訊或不正確的音訊。

   以「就緒」狀態準備音軌並通知音軌。

**版本1.4.38** (1.4.38.860)

* (ZD #29281)- iOS:將AdSystem和Creative Id新增至CRS請求

基於CRS標準化規則的CRS請求中創意ID和AdSystem的使用

* (ZD #29176)- `PTAdPolicyDeligate` `satAdBreakAsWatched:position`當機

現在已處理由於空AdBreak而造成的當機。

* (ZD #30125)-程式化廣告無法在iOS平台中運作

在iOS中新增程式化廣告支援。

* (ZD #30782)- #EXT-X-PROGRAM-DATE-TIME通知

EXT-X-PROGRAM-DATE-TIME標籤與即時DRM串流不會引發計時中繼資料事件。

**1.4.37版(1.4.37.842)**

* (ZD #28950)- VOD播放問題

串流中# EXT-X-PLAYLIST-TYPE標籤設定為「事件」而非VOD時的播放問題

* (ZD #29281)- iOS:將AdSystem和Creative Id新增至CRS請求

根據CRS標準化規則在CRS請求中使用Creative Id和AdSystem。

* (ZD #29462)- A&amp;E VOD中的StuochHub廣告造成iOS應用程式當機

**1.4.36版(1.4.36.835)**

* (ZD #29418)-持續時間0(#EXT-X-CUE-OUT:0.000)的提示會導致iOS TVSDK停止或當機播放。

問題已修正，並可正確開始播放。

* (ZD #29462)-造成iOS TVSDK當機的VOD中的廣告。

問題已修正。 iOS TVSDK會提高`exception(AUDNetworkAdInfo::initWithAdId)`，但不會處理它。 例外是由於空的廣告ID。

* (ZD #29281)-將AdSystem和Creative ID新增至CRS要求。

在1401和1403個請求中加入AdSystem和CreativeId作為新參數（所有其他參數保持不變）。

**1.4.35** (1.4.35.830)版

* (ZD #27830)-需要以程式設計方式決定iOS中隱藏字幕和字幕之間的差異。

TVSDK現在會公開兩種類型，可用來篩選必要的標題類型。

* (ZD #29160)- EXT-X-CUE-OUT廣告提示無法在TVSDK iOS上正確地接入。

現在正在播放EXT-X-CUE-OUT Midroll廣告。

* (ZD #29100)-當使用者在影片結束時，應用程式當機。

修正與同步相關的多次當機。

* (ZD #28785)、(ZD #27712)和(ZD #25076)- iOS應用程式在大型即時事件期間當機。

修正與同步相關的多次當機。

**版本1.4.34** （iOS 6.0+專用1.4.34.815）

* (ZD #28481)- FER中斷，因為這些FER串流的廣告插播結束時附加了不正確的鍵

對於FER串流，廣告分段前的索引鍵會插入廣告分段結束後的索引鍵。 此問題已解決，方法是在廣告插播的結尾附加&#x200B;*最後一個看見的索引鍵*。

**版本1.4.33** （iOS 6.0+專用1.4.33.803）

* (ZD# 21701)啟用子帳戶的CRS

依據CRS後端的需求，傳送1401個CRS請求的原始創意URL，而非標準化URL，以啟用此功能。

* (ZD# 26218)- PSDKResources.bundle載入問題

此問題已解決，方法是更新資源載入，以便從所有可用的捆綁包中查找。

* (ZD# 27460)Midroll首次廣告呼叫-POST至`cdn.auditude.com`返回403。

新的CDN帳戶無法處理POSTCDN請求。 此問題已解決，方法是更新程式碼，使`cdn.auditude.com`廣告要求成為GET，而非POST。

**1.4.32版** （iOS 6.0+專用1.4.32.792）

* (ZD# 27132)支援VMAP廣告插播的小數值。

當內容未依定義的廣告插播分段時，整數會造成非預期的廣告位置。 此問題是不將小數值轉換為整數而解決的。

* (ZD# 27189)具有EXT-X-DINSTRUCTION-SEQUENCE標籤的AES內容無法正確播放。

將標籤放置在播放清單的開頭，即可解決此問題。

**1.4.31版** （iOS 6.0+專用1.4.31.785）

* (ZD# 24528)實施TVSDK帳單使用量度

如需詳細資訊，請參閱[帳單量度]。

* (ZD# 24642)TVSDK的畫中畫支援

在某些情況下無法正常運作的畫中畫功能已經修正。

* (ZD# 25246)錯誤的廣告插播信號

這個問題是透過對齊變型清單上的不連續標籤來解決的。

* (ZD# 26218)當嘗試將PSDKLibrary.framework加入用戶端的應用程式架構時，應用程式建立程式變得複雜

此問題已依要求封裝PSDKLibrary.framework而解決。

* (ZD# 26364)CRS廣告的多CDN支援

如需詳細資訊，請參閱CRS廣告傳送的多個CDN支援。

* (ZD# 27028)在iOS 10中播放某些串流的延遲。

此問題已解決，方法是針對沒有M3U8擴充功能的串流提供因應措施。

**1.4.30版** （iOS 6.0+專用1.4.30.754）

TVSDK在此版本中已解決下列問題：

* (ZD# 24180)新增自訂標題以允許清單。

新的自訂標題已新增至TVSDK允許清單。

* (ZD# 25016)設定ABR控制參數時，會隨機選取容錯流

當ABR設定在包含容錯URL的串流上提供initialBitrate設定時，可依順序維持ABR串流，以解決此問題。 這樣將避免播放故障切換流而不是主流。

* (ZD# 25076)PTAuditudeAdResolver loadComplete上的當機

已修正在快速啟動／停止多個含廣告的PTMediaPlayer例項時發生當機的問題。

* (ZD# 25960)沒有額外的訂閱標籤，會觸發中繼資料變更通知廣播

訂閱標籤出現在資訊清單中第一個區段之前時未收到通知的問題已經修正。

* (ZD# 26084)PSDK投擲106000.101000.-11833解碼器從最後一個廣告插播轉換回娛樂內容時未發現錯誤

當來自VMAP的最後一個廣告插播開始時間落在總持續時間完成之前時，在某些情況下，直到最後一個廣告插播結束後，才會插入索引鍵。 此問題已修正。

* 視訊心率程式庫(VHL)已更新至1.5.9版，以解決下列問題：

* (ZD #22351)VHL —— 分析：即時視訊資產持續時間

此問題已解決，方法是將assetDuration API新增至PTVideoAnalyticsTrackingMetadata，以更新即時／線性串流的資產持續時間，並提供檢查即時串流的邏輯。

* (ZD# 22675)VHL —— 分析：更新即時視訊資產持續時間

此問題與ZD #22351相同。

* (ZD #25908)VHL —— 分析：Adobe心率事件當機

此問題已解決，方法是將實作更新為使用iOS 1.5.9版VHL的最新版本，以改善穩定性和效能。

* (ZD #25956)VHL —— 分析：重複播放視訊時當機

此問題與ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)第三方廣告未播放

此問題已解決，方法是移至CRS v3 URL結構，將區域ID包含在重新封裝的URL中。

* (ZD #25183)在tvOS和iOS上播放DRM的問題

此問題已解決，因為它支援多DRM支援所需的多個關鍵標籤。

* (ZD# 25334)TVSDK無法播放cDVR共用內容

此問題已透過防止TVSDK將空字串轉換為絕對URL而解決。

* (ZD# 25347)在AVURLAsset上設定自訂HTTP標題

已新增透過PTNetworkConfiguration類別對其區段請求的自訂標題的支援。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多個廣告追蹤呼叫

此問題已解決，方法是更新時間軸管理器，以在建立多個播放器時監聽特定物件的通知。

* (ZD #24758)PTManifestLogger不支援iOS 8

將記錄器實用程式庫更新為7.0版部署目標，以解決此問題。

* (ZD #24775)由於廣告而延遲的串流

此問題已透過正確計算事件播放清單上的持續時間漂移而解決。

* (ZD #24799)部分集目未在iOS應用程式上播放

當WebVTT檔案受地域限制時，使用本機Web伺服器進行字幕處理，以解決此問題。

**iOS 6.0+版本1.4.27** (1.4.27.711)

* (ZD #24089)-針對長DVR串流進行廣告解析的最佳化

此問題已解決，方法是新增多項最佳化，以縮短在即時／線性串流中處理DVR視窗所需的時間。

* (ZD #21554)-應用程式類型= video/mp4未引發的TVSDK錯誤信標

此問題已解決，讓播放器針對無效資產格式，ping正確的錯誤追蹤URL。

* (ZD #24424)- EXC_BAD_ACCESS KERN_INVALID_ADDRESS類型的當機源自於PSDKLib內部，適用於較新硬體裝置的iOS。

已修正因解除配置的媒體播放器例項而發生的當機問題，當播放在不同串流之間快速切換時。

* (ZD #24575)- 32位元裝置上的TVSDK當enableDebugLog=true時當機

記錄啟用時導致32位元裝置當機的記錄格式問題已經修正。

**iOS 6.0+版本1.4** .26(1.4.26.702)

* (ZD# 20213)- XCode7需要動態／模組化TVSDK FW

通過更新具有模組支援的庫來修復

**iOS 6.0+版本1.4.25** (1.4.25.684)

* (ZD #19629)-進入Airplay至ATV 4時即時視訊暫停

此問題已解決，方法是在移除舊項目後，但在新增項目至AVQueuePlayer之前新增等候期。 沒有等候期，通知會傳送至不正確的項目。

* (ZD #19856)-預設啟用時不顯示字幕

webvt播放清單中導致字幕無法正確顯示的問題已修正。

* (ZD #21590)-最新原始建置中的視訊效能與追蹤

VideoAnalytics中遺失視訊長度的問題已經修正。

* (ZD #20202)-設定自訂字幕樣式會使iOS應用程式當機

此問題已解決，方法是在設定子標題樣式時新增其他空物件檢查。

* (ZD #20709)-視訊開始追蹤中報告為0的視訊長度

此問題與(ZD #21590)相同。

* (ZD #22280)- Analytics視訊長度設定為0

此問題與(ZD #21590)相同。

* (ZD #22592)- Primetime的Airplay問題

此問題與(ZD #19629)相同。

* (ZD#22922)-適用於iOS的手動位元速率切換

此問題已解決，方法是提供指定最大位元速率的選項。

* (ZD #23084)-僅限IPv6網路的Apple Compliance

Apple不建議使用的符號已移除。

**iOS 6.0+版本1.4.24** (1.4.24.661)

* ZD #2548)- Primetime對行動裝置互動式廣告的支援- VPAID 2.0

如果VPAID廣告無法播放，請將邏輯更新為取消隱藏播放器檢視，以解決此問題。

* (ZD #20101)-自訂章節實作會在廣告播放期間觸發章節開始事件

此問題已解決，方法是更新VideoAnalyticsTracker，以在章節和非章節邊界之間轉換時正確偵測章節開始／完成。

* (ZD #20784)-分析：觸發內容完成即時視訊轉場

此問題已解決，方法是新增邏輯以手動觸發視訊追蹤工作階段中的內容完成。

已更新下列程式庫：

* AdobeMobile程式庫至4.10.0
* VHL程式庫至1.5.6
* VHL-Nielsen資料庫至1.6.7
* (ZD #21855)-字幕在中段後不播放

在此問題中，重複的不連續標籤會導致字幕在中間卷之後無法顯示。 此問題已透過移除彼此相鄰的不連續標籤來解決。

* (ZD #21994)- PTHLSUtils中的字串超出範圍

當EXT-X-KEY的URL被引號包圍時，最可能造成當機的原因。

* ZD #22074)-每分鐘在iOS上發生一次AUDVAST當機

在1.4.23版中，由於VAST重新導向URL中存在不安全字元而造成的當機已修正。 不過，TVSDK仍會略過這些廣告。

這個問題是透過處理不安全的字元以及允許播放廣告來解決。

* (ZD #22694)- PTMediaPlayer。  視圖由播放器隱藏

如果VPAID廣告無法播放，請將邏輯更新為取消隱藏播放器檢視，以解決此問題。

**iOS 6.0+版本1.4.23** (1.4.23.641)

* (ZD #18016)- Primetime SDK無網路狀況不佳之回應

此問題已解決，方法是改善AVFoundation發生嚴重錯誤時的錯誤通知，並允許應用程式在錯誤後處理重新啟動。

* (ZD #20580)- PTSplicerManager中的當機

此問題已解決，因為它針對造成當機的並行問題提供額外的保護。

* (ZD #21782)- iOS錯誤代碼10100

TVSDK在Adobe存取DRM串流上開始播放時傳回101000錯誤的問題已經修正。

* (ZD #21889)-線上廣告和離線內容播放失敗

已修正AES加密離線內容上的廣告失敗的問題。

* (ZD #22074)-每分鐘在iOS上發生一次AUDVAST當機

此問題已透過改善處理URL中含有無效字元的協力廠商VAST廣告標籤而解決。

* (ZD #22257)- TVSDK無法播放DRM串流

TVSDK在Adobe存取DRM串流上開始播放時傳回101000錯誤的問題已修正。

**iOS 6.0+版本1.4.22** (1.4.22.627)

* (ZD #18709)-適用於iOS的TVSDK當機

某些Adobe存取DRM保護串流發生當機的問題已經修正。

* (ZD #18850)-根據CRS規則更新創意選擇邏輯

此問題已透過新增。json設定檔案來指定創意選擇的優先順序來解決。

* (ZD #19770)-受保護的AES視訊饋送不再播放

已修正某些302個重新導向串流無法播放的問題。

* (ZD #19629)-進入Airplay至ATV 4時即時視訊暫停

此問題已解決，方法是新增在Apple TV 4裝置開啟播放時暫停即時視訊的因應措施。 此問題似乎是AppleTV 4問題。

* (ZD #21119)- TVSDK在廣告播放後停止

使用廣告插入時，已新增支援序列IV的AES加密串流。

* (ZD #21125)-提早從即時／線性廣告插播返回

已新增支援，可在播放廣告插播至完成之前，從廣告插播返回。 透過自訂資訊清單標籤指出提早傳回。

* (ZD #21224)- Airplay支援Akamai的Token化串流

API已新增至PTNetworkConfiguration類別，以附加Cookie作為特定Akamai Token化串流區段的URL參數。

* (ZD #21287)-無關記錄

即使在停用記錄功能時，Xcode主控台中依預設會顯示某些記錄陳述式的問題已經修正。

* (ZD #21446)-廣告中斷事件有時不是由TVSDK觸發

在EVENT串流中，在舊版建置中無法正確觸發廣告中斷。 此組建版本可解決此問題。

**iOS 6.0+版本1.4.21** (1.4.21.605)

* (ZD #20749)-備援會跳過非空的VAST回應；引發額外廣告追蹤URL

已解決備援廣告上重複ping的問題。

**iOS 6.0+版本1.4** .20(1.4.20.590)

* (ZD #18639)- TVSDK在冗長的熱錄制資產上使用過多的CPU/資源

CPU/資源使用量過高已修正為兩個層級。 首先，讓時間更新函式在全域佇列上執行，而非主執行緒，並最佳化CPU使用先前處理和快取的m3u8來剖析資訊清單。

* (ZD #19349)-調節網路連線時，會略過前滾廣告。

此問題已解決，方法是提供逾時事件(requestTimeout)至應用程式和adMetadata。  adRequestTimeout API，以覆寫預設的10秒逾時。

* (ZD #19446)-即時串流上遺失通知

此問題已解決，因為應用程式可在即時串流上訂閱EXT-X-PROGRAM-DATE-TIME。

* (ZD #19459)-使用PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions準備替代音訊時當機
* (ZD #19460)-當機- `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此問題與Zendesk #19459相同。

* (ZD #19574)- TVSDK不會傳回DRM或非DRM內容的M3U8回應資料

在PTMediaPlayerItem.prepareToPlay中初始載入manifest檔案時，如果載入資訊清單失敗，TVSDK不會向應用程式報告失敗回應的正文。

此問題已解決，因為TVSDK會將失敗回應報告為應用程式的錯誤。

* (ZD #19615)-備援邏輯無法運作

在目前的實作中，備援廣告已略過，除非這些廣告採用m3u8格式，否則不會重新封裝。 此問題也已解決，因為新增了重新封裝備援廣告的支援。

* (ZD #19770)- TVSDK無法播放任何受保護的AES內容，並重新導向302

重新導向問題已修正，因為重新導向URL在可用來剖析資訊清單之前，已被cleanConnectionData清除。

* (ZD #19856)-預設啟用時，字幕無法針對某些位元速率顯示

此問題已解決，方法是針對未顯示字幕的串流區段處理iOS錯誤。

* (ZD #19868)-當無效創意素材被販賣時，TVSDK會當機

已修正TVSDK中錯誤地解除配置大型剖析器例項的當機問題。

* (ZD #20180)-偶爾會略過VPAID廣告

JavaScript mime類型並非一律包含或視為有效的mime類型。 此問題已透過將JavaScript納入為有效的MIME類型而解決。

* (ZD #20749)-備援會跳過非空的VAST回應；引發額外廣告追蹤URL

部分創意素材未重新封裝的問題已經修正。

**iOS 6.0+版本1.4** .19(1.4.19.563)

* ZD #18639)- TVSDK在冗長的熱錄制資產上使用過多的CPU/資源

此問題已解決，方法是將DRM m3u8播放清單重寫最佳化，以快取先前已重寫之播放清單的位元。 當您播放即時m3u8串流時，這點最相關，而m3u8會在每次區段下載後下載。

* (ZD#18956)- player.drmManager在iOS Demo Player中設定中斷點時為nil

此問題已解決，方法是更新PTMediaPlayer.drmManager API實作，從DRM架構中擷取DRManager。

**iOS 6.0+版本1.4** .18(1.4.18.557)

* (ZD #18844)在iOS播放器中追蹤即時內容的播放磁頭。

此問題已透過允許應用程式設定其自己的播放頭值而解決。

* (Zendesk #18518)-如果未指定視訊名稱，TVSDK的名稱預設為* PSDK型播放器。*

此問題已透過移除播放器名稱的預設值來解決。

**iOS 6.0+版本1.4** .17(1.4.17.545)

* (Zendesk #2228)-增強TVSDK，傳回資訊清單擷取的JSON回應

DRM Framework不會在內容不是M3U8時傳送錯誤，而會傳回nil DRMetadata。 當M3U8_PARSER_ERROR通知發生時，新增中繼資料以公開內容，以解決此問題。

* (Zendesk #2231)-擷取MediaPlayerNotification中無法使用的資訊清單時傳回錯誤

與Zendesk #2228的解析度相同

* (Zendesk #3304)-未填充VAST 3.0 `[ERRORCODE]`宏

追蹤URL開頭有空格時，Auditude SDK無法傳送ping的問題已經解決。

* (Zendesk #17294)-當機SecKeyRawSign

客戶程式碼使用金鑰鏈時，可能發生當機的問題已解決。

* (Zendesk #18008)-支援iOS8+的Cookie，以支援Token化串流

Akamai Token化的串流需要在區段請求上傳送Cookie，而這在iOS 7和舊版上是無法做到的。 從iOS 8開始，Apple已新增API，允許針對區段請求傳遞Cookie。 TVSDK現在提供此支援。 此外，也新增了傳送使用者代理的支援（若有的話）。

* (Zendesk #18166)- TVSDK 1.4.15在使用含dSYM檔案選項的DWARF編譯時會發出數百個警告

所有警告都已解決。

**注意**:已新增TVSDK的tvOS相容程式庫。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S在播放期間當機

回復OKHTTP對CRSauditude的依賴性，因為TVSDK現在直接使用httpurlconnection而非curl。 在進行另一個JNI呼叫前，清除例外即可解決此問題。

* (Zendesk #4487)-追蹤內容線性頻道

線上性串流播放工作階段期間重新初始化視訊心率追蹤器，以解決此問題。

* (Zendesk #17919)- Android —— 內容搜尋導致心率錯誤

問題是當一章中有搜尋時，解決錯誤狀態中的心跳

* (Zendesk #18053)-使用TVSDK的應用程式在Marshmallow上當機

當TVSDK程式庫使用進行YUV `->` RGB色彩轉換的neon程式碼時，TVSDK會在Android M OS上當機。 此問題已解決，方法是使用`code`的非Neon版本更新導致此問題的函式。

* (Zendesk #18072)- Android M —— 應用程式當機

當檢查描述檔和層級是否受支援時，當呼叫MediaCodecList和MediaCodecInfo API時，會發生此損毀。 Adobe正在尋求谷歌對更多洞察力的支援。 此問題已解決，方法是提前載入所有轉碼器資訊，以避免只在需要轉碼器資訊時呼叫這些API。

* (Zendesk #18074)-在Nexus與Android 6.0上無法使用阿拉伯文字幕

此問題已透過支援Android CTS字型圖而解決。

**iOS 6.0+版本1.4** .15(1.4.15.512)

**注意**:Nielsen模組已從TVSDK組建版本移除，但TVSDK將在不久的將來更新，並新增Nielsen整合模組。

* (ZD #2228)-擷取MediaPlayerNotification中無法使用的資訊清單時傳回錯誤

已新增中繼資料，以在通知M3U8_PARSER_ERROR發生時公開內容。

* (ZD #4437)-Adobe PrimetimeSDK內當機

修正準備字幕／替代音訊時報告的當機問題。

* (ZD #4487)-追蹤內容的線性頻道

允許線上性串流播放作業階段期間重新初始化視訊心率追蹤器。

**iOS 6.0+版本1.4** .14(1.4.14.498)

* (ZD #17260)- Crash on playlistManagerForURL

已修正併發問題造成的間歇性當機問題。

**1.4.13版** (iOS 6.0+)

* (ZD #3304)-未填充VAST 3.0 `[ERRORCODE]`宏

   * 如果內嵌   廣告的創意不佳。
   * `[ERRORCODE]` 宏將進行URL編碼。

* (ZD #3865)心率與IMA廣告整合

已修正報告錯誤視訊長度的錯誤。

* 更新TVSDK示範播放器以支援iOS 9

若要正確支援iOS 9，您必須設定「應用程式傳輸安全性」的例外。 為了示範，ATS已完全停用。

**iOS 6.0+版本1.4.12** (1.4.12.464)

* (ZD #4521)CRS測試用戶端和SSAI

修正3P URL中的反向MD5錯誤。

**iOS 6.0+版本1.4.12** (1.4.12.463)

* (ZD #2751)CSAI和CRS /增強：處理特定媒體檔案URL中的動態元素。

更新Creative重新封裝服務，以使用動態創意URL正確處理廣告。

* (ZD #3654)1.3.4.166後PSDK版本的記憶體洩漏

在iOS 8.2裝置上定期播放drmFramework時，已修正記憶體洩漏

* (ZD #3988)首次播放後，當尋找回卷時會略過前卷

已修正錯誤，以便正確停用廣告原則。

* (ZD #4017)請求iOS API，以強制在反向搜尋上播放廣告

已解決ZD #4279的修補程式

* (ZD #4279)iOS和案頭上的HLS TVSDK廣告插入-302重新導向問題

修正廣告資產使用相對重新導向URL時的錯誤

**iOS 6.0+版本1.4.9** (1.4.9.427)

* (ZD #3075)網際網路連線能力問題- iOS

已新增通知以偵測播放何時停止。

* (ZD #3193)在TVSDK中要求描述檔變更API

更新PTPlaybackInformation以顯示更新的indicatedBitrate。 更新BITRATE_CHANGE通知，讓M3U8報告的位元速率更具時間可靠性和精確性。

* (ZD #3324)黃金時段廣告在VMAP中沒有廣告媒體時的報告問題

支援ping空的廣告插播追蹤URL,TVSDK現在會確認廣告插播開始並完成ping空的廣告插播。

**1.4.8版** (1.4.8.402)

* (ZD #3158)IOS 7在完整事件重播中當機

**1.4.7版** (1.4.7.382)

* (ZD #2197)追蹤廣告錯誤。 新增資產通知無法載入資訊清單。
* (ZD #2894)播放器在播放期間發出4個頂層資訊清單請求。
* (ZD #2992)Auditude報告奇怪的持續時間和標識符。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)追蹤廣告錯誤。 新增資產通知無法載入資訊清單

**版本1.4.5** (1.4.5.283)

* (ZD #2141)TreeHouse應用程式的Analytics實作，新增`AdobeAnalyticsPlugin.a`程式庫以建立套件。
* 視訊心率程式庫更新至1.4.1.2
* (PTPALY-4226)（與ZD #2423有關）執行DRM重置可導致刪除應用程式文檔資料。

**版本1.4.4** (1.4.4.242)

* 視訊心率程式庫(VHL)更新為1.4.1。

* (ZD #2435)有關分析需求更新的TV SDK檔案

**1.4.2版** (1.4.2.210:iOS 6.0+)

* (ZD #1129)`_player.currentItem.audioOptions`返回空白
* (ZD #2109)Primetime PSDK 1.4.1.125不適用於Xcode 5.1.1
* (ZD #2137)無法載入DRM中繼資料時，iOS上的PSDK當機

**1.4.1版**(1.4.1.125)

* (ZD #1107)CocoaLumberjack重複符號
* (ZD #1644)修改iOS使用者代理以進行定位和報告
* (ZD #1850)iOS SDK中包含的Cocoa Lumberjack檔案
* (ZD#1908)如果自訂標籤超過1,PSDK會忽略自訂標籤

**1.4.0版** (1.4.0.32)

* Zendesk #1024 —— 透過資訊清單從串流移除廣告的功能

## 裝置認證與支援{#device-certification-and-support}

>[!NOTE]
>
>TVSDK支援下列功能：**not**:
>
>* 在任何平台或版本上都能執行慢動作。
>* 即時戲法遊戲。


**1.4.43版**

* TVSDK 1.4.43已通過iOS 11認證。

**1.4.29版**

* TVSDK 1.4.29已通過iOS 10認證。

**1.4.28版**

* TVSDK 1.4.28已通過iOS 10 Beta 7認證。
* DRM支援透過新增`forceHTTPS`和`isForcingHTTPS` API來強制HTTPS。
* 將VHL程式庫更新為1.5.8、將Mobile程式庫Adobe為4.8.4，以及將記錄器公用程式程式庫更新為7.0版部署目標。

**1.4.19版**

本版TVSDK已通過iOS和tvOS的FairPlay支援認證。

**1.4.17版**

* tvOS

   此版本的TVSDK包含對tvOS的支援，並已通過未加密HLS串流的認證。

   **注意**:請記住下列編譯准則：

   * TVSDK tvOs支援僅限非AdobeDRM加密串流。 您必須移除tvOS建置設定中drmNativeInterface.framework的參考。 仍支援AES加密串流。
   * Apple要求所有Apple TV應用程式都必須啟用位元程式碼，因此您必須在專案設定中開啟此旗標。

## 已知問題和限制{#known-issues-and-limitations}

* 由於iOS TVSDK 3.6以後版本不再使用iOS UIWebView類別：
   * VPAID廣告在iPad 13中不會如預期般播放。
   * 配套廣告將無法如預期般播放。

* 在iOS TVSDK中，所有廣告都會銜接到內容資訊清單中。 廣告行為是透過根據內容和廣告區段的持續時間進行搜尋來實施。 因此，如果區段持續時間不準確，搜尋不一定會以廣告插播開始或結束的確切畫格結束。 即使持續時間在影格上，平台本身對搜尋仍有容許度，而且可能會顯示一些影格或廣告或內容。 這是平台的限制，也是iOS上廣告插入與TVSDK搭配運作的方式。
* 在本例中，跳過的決定發生在搜尋事件上。 但是，由於資訊清單中的廣告區段持續時間無法精確表示廣告的實際持續時間，因此搜尋不準確影格。 因此，在套用廣告原則時，您會看到幾個廣告框架。
* iOS 11上無法播放授權旋轉影片，而iOS 9.x和iOS 10.x上也能正常播放。
* 在VPAID 2.0支援中，如果播放在AirPlay上是作用中，則會略過VPAID廣告。
* 當最小目標設為iOS7（或更新版本）時，drmNativeInterface.framework無法正確連結。
解決方法：明確指定libstdc++.6.dylib庫，如下所示：轉至Target->Build Phases->Link Binary With Libraries，並新增libstdc++.6.dylib。
* 未插入替換API的滾動後廣告。
* 在廣告中斷中搜尋（未從中退出）會發出重複的廣告開始和廣告中斷通知
* 設定currentTimeUpdateInterval沒有任何作用。
注意：在某些iOS版本中，作業系統不會自動載入PSDKLibrary.framework內的資源。 請務必手動將PSDKResources.bundle複製至應用程式的Bundle資源：轉到「構建階段」並複製捆綁包資源。
* 無法使用Xcode 8或更低版本建立參考應用程式。 iOS TVSDK 1.4.41版之後，請使用Xcode 9進行編譯。
* VPAID廣告不會遵循delayAdLoadingTolerance值。
* 24077-對於具有字幕的某些HLS內容，播放器會在「停止」或「重設」方法上當機。
* 當啟用「僅限時間廣告」解決時，無法使用詳細的錯誤通知。
* 錯誤通知會根據廣告解析時間記錄，而非根據廣告順序記錄。
* HEVC支援在此版本中有下列限制
   * 不支援DRM
   * CC(CEA 608/708)不支援，因為CMAF不支援它。
   * 4K支援尚未提供。
   * ID3標籤不支援，因為CMAF不支援它。
   * 未驗證未經過混合的Live HEVC流。
   * 未驗證HEVC Ads支援。
* 啟用JIT並將容限設為10秒後，在出現VMAP->VAST重新導向廣告時，第一個midroll廣告插播時不會看到VAST呼叫。
* 為了讓廣告解析度逾時正常運作，每當即時串流播放期間更新播放清單時，播放器就會預期20秒內會有銜接播放清單。 如果在所述間隔內未接收到銜接播放清單，則拋出內部錯誤並且播放器停止。

## 實用資源{#helpful-resources}

* [iOS版TVSDK 3.4程式設計人員指南](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [TVSDK iOS 3.4 API參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。
