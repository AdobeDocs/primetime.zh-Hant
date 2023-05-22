---
title: 《 TVSDK 3.13 foriOS發行說明》
description: 《 TVSDK 3.13 foriOS發行說明》介紹了TVSDKiOS3.13中的新增或更改內容、已解決和已知問題以及設備問題。
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# 《 TVSDK 3.13 foriOS發行說明》 {#tvsdk-for-ios-release-notes}

《 TVSDK 3.12 foriOS發行說明》描述了TVSDKiOS3.12中的新增或更改內容、已解決和已知問題以及設備問題。

## 系統和軟體要求 {#system-software-requirements}

在下載iOS3.12之前，請確保硬體、作業系統和應用程式版本符合以下要求：

作業系統：iOS8.0或更高版本。

## iOSTVSDK 3.13

該版本為LIVE,VOD和FER流提供對DEMUXED &#39;HLS/CMAF&#39;（前滾，midroll和poslor）廣告的支援。

有關解決客戶報告問題的方法，請參見 [已解決的問題](#resolved-issues)。 有關限制，請參見 [已知問題和限制](#known-issues-and-limitations)。

### 以前版本中的新功能和修復 {#whats-new-previous}

**iOSTVSDK 3.12**

已修復在播放15分鐘後即時流失敗的問題。

**iOSTVSDK 3.11**

為客戶問題提供修復， `isFallbackOnInvalidCreativeEnabled` 方法 `customParams` 導致應用程式崩潰。

**iOSTVSDK 3.10**

* 已修復TVSDK播放器未觸發的問題 `PTMediaPlayerStatusError` 網路不可用時通知。

**iOSTVSDK 3.9**

* 已修復VTT字幕無法回放導致應用凍結的問題。

* iOSTVSDK 3.9包括更新的個性化傳輸證書。

**iOSTVSDK 3.8.0.83修補程式**

修補程式具有更新的個性化傳輸證書。

**iOSTVSDK 3.8**

iOS13遵守和處理iOS13 `UIWebView` API棄用。

**iOSTVSDK 3.7**

在同時發出許多廣告解析請求時，播放停止的場景的熱修復程式。

**iOSTVSDK 3.6**

**類的vastXML屬性中的修復`PTNetworkAdInfo`**

的 `vastXML` 未正確設定屬性，正在返回零值。

**iOSTVSDK 3.5**

**啟用後台音頻**

*將應用配置為在音頻進入後台時繼續播放。*

要啟用此功能，必須設定新API `audioPlaybackInBackground` 的 `PTMediaPlayer` 類。 啟用此API後，您的應用可以播放後台音頻。

**iOSTVSDK 3.4.0.19（修補程式）**

此版本具有針對廣告故障切換方案中發生的應用程式崩潰的修復程式。

**iOSTVSDK 3.4**

**廣告解析超時**

* 使用TVSDK 3.4，用戶現在可以為整體廣告解析度和清單下載設定超時值。 如果在給定超時內某些廣告未解決，則TVSDK將播放剩餘廣告。

* `PTAdMetadata: adRequestTimeout` API已棄用，將被刪除。 預設值已設定為35秒。

* 在 `PTAdMetadataClass: adResolutionTimeout`   — 總體廣告解析調用adManifestTimeout超時 — 廣告清單下載超時。

**收入優化**

使TVSDK能夠識別與廣告插入工作流相關的問題區域，以便向分析最終選擇點報告。

**版本3.3**

TVSDK 3.3現在符合iOS11 SDK。 所有過時的API都已用合適的替代方案替換。

**版本3.2**

**其他日誌記錄支援（階段2）**

添加了對錯誤通知的支援，在以下情況下：

* HLS版廣告使用的級別比內容高。

* 排除僅音頻變數。

* VAST/VMAP請求失敗。

**版本3.1**

* **其他日誌記錄支援**
添加了對說明性通知的支援（如果廣告播放失敗）。

* **已添加 [!DNL Fairplay] 加密的CMAF流支援**
   [!DNL Fairplay] 現在支援使用AVC編解碼器回放的加密CMAF流。

**3.0.1版**

此版本中沒有新功能或增強功能。

**版本3.0**

* TVSDK 3.0支援HEVC流。

* 及時 — 將廣告解析得更接近廣告標籤。

已添加 `enableDelayAdLoading` 用於啟用JIT的App級介面上布爾類型的屬性。 如果 `enableDelayAdLoading` 不，它會 `setadMetadata.delayAdLoading`到True（PTAdMetadata介面的屬性）。

啟用此屬性後，TVSDK會根據定義的容差值在其位置之前解析每個廣告中斷。 預設情況下， `delayAdTolerance` 設定為5秒。

**1.4.45版**

為遵守Xcode10,TVSDK已從 `libstdc++` 至 `libc++`，因此支援的最低版本為iOS7。 早些時候是iOS6號。

**1.4.44版**

此版本中沒有新功能或增強功能。

**1.4.43版**

* 像電視一樣的體驗，能夠在廣告中間加入而不觸發部分廣告跟蹤。\
   示例：用戶在90秒廣告中間（40秒）加入，其中包括3個30秒廣告。 這是第二個廣告的10秒。

   * 第二廣告在剩餘持續時間（20秒）後播放第三廣告。
   * 未觸發部分廣告（第二個廣告）的廣告跟蹤器。 只觸發第三個廣告的追蹤器。

* 已添加 `enableVodPreroll` PTAdMetadata介面中布爾類型的屬性。 該屬性可用於在VoD流上啟用預滾。 如果 `enableVodPreroll` 不，PSDK不播放預播。 但這對中盤沒有影響。 預設值 `enableVodPreroll` 是。
* `closedCaptionDisplayEnabled` API `PTMediaPlayer` 從iOSv1.4.43開始，介面被標籤為不建議使用。 確定給定的標題是否可用 `PTMediaPlayerItem`，檢查 `subtitlesOptions` 物業 `PTMediaPlayerMediaItem`。

**1.4.42版**

此版本中未添加任何新功能。 有關已修復問題的清單，請參見 [已解決的問題](#resolved-issues)。

**1.4.41版**

API更改：

* **是安全的**:引入了新的APIisSecure，以保護播放器不會記錄和引發錯誤。 預設值為true。

* **allowExternalRecording**:引入了新的API以允許對安全內容進行空播鏡像。 Airplay鏡像被視為記錄 `allowExternalRecording` 值必須設定為 `True`，允許播放鏡像或設定為 `False` 停止播放鏡像以獲取安全內容。 預設情況下， `value` 是真的。

**1.4.40版**

沒有新功能。

**1.4.39版**

* iOSTVSDK經VHL2.0.1和尼爾森VHL2.0.1認證。

* iOSTVSDK被更新，以從新Akamai主機發出CRS請求 `primetime-a.akamaihd.net`。

* 新的主機名配置提供了通過HTTP和HTTPS(SSL)的CRS資產傳遞，其規模更大。

**1.4.36版**

在iOSTVSDK中整合和認證VHL 2.0 :減少 `VideoHeartbeatsLibrary` 通過降低API的複雜性來實現。

**1.4.34版**

**網路廣告資訊**

TVSDK API現在提供了有關第三方VAST響應的其他資訊。 中提供了廣告ID、廣告系統和VAST廣告擴展 `PTNetworkAdInfo` 可訪問的類  `networkAdInfo`  Ad Asset上的屬性。 此資訊可用於與其他Ad Analytics平台整合，如 **Moat分析**。

**1.4.31版**

* **計費度量** 為了適應那些只想按使用付費而不是按固定費率付費的客戶，Adobe收集使用量度，並使用這些度量來確定向客戶收取的費用。

   每次TVSDK生成流啟動事件時，播放器開始定期向Adobe的計費系統發送HTTP消息。 該週期稱為可計費持續時間，對於標準VOD、pro VOD（啟用中間廣告）和即時內容可以不同。 每種內容類型的預設持續時間為30分鐘，但您與Adobe的合同將確定實際值。

* **CRS廣告的多CDN支援** TVSDK現在支援Multi-CDN用於CRS廣告。 通過為CRS廣告提供FTP詳細資訊，您可以指定CDN位置，而不是預設Adobe擁有的CDN，如 [!DNL Akamai]。

**1.4.29版**

在 `PTSDKConfig` 類， `forceHTTPS` 已添加API。

的 `PTSDKConfig` 類提供了對向Adobe Primetime和Video Analytics伺服器發出的請求強制執行SSL的方法。 有關詳細資訊，請參見 `forceHTTPS` 和 `isForcingHTTPS` 類的方法。 如果清單通過HTTPS載入，TVSDK將保留HTTPS的內容使用，並在從清單載入任何相對URL時考慮此用法。

>[!NOTE]
>
>對第三方域（如廣告跟蹤像素、內容和廣告URL）的請求以及類似的請求不會被修改，內容提供者和廣告伺服器有責任提供通過HTTPS支援的URL。

**1.4.18版**

黃金時段iOSTVSDK現在支援VPAID 2.0 JavaScript創意，以實現豐富的互動式流中廣告體驗。 有關VPAID 2.0的詳細資訊，請參閱VPAID廣告支援。

**1.4.17版**

* 電視作業系統

   TVSDK支援tvOS本機應用程式。
* 可以播放以下類型的內容：

   * 視頻點播
   * 實況
   * AES-128
   * 備用音頻和字幕
   * FER

* 可以顯示以下類型的廣告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 當前不支援以下功能：

   * Digital Rights Management(DRM)
   * 廣告橫幅
   * 電視標籤語言(TVML)

**1.4.13版**

>[!NOTE]
>
>尼爾森模組已從TVSDK版本中刪除，TVSDK將很快用新的尼爾森整合模組更新。

**廣告回退，廣告選擇邏輯中的菊花鏈(Zendesk #3103)**

對於啟用回退規則的VAST廣告（建立性）,TVSDK將MIME類型無效的廣告視為空廣告，並嘗試使用備用廣告。 您可以配置回退行為的某些方面。 有關詳細資訊，請參閱VAST和VMAP廣告的廣告回退。

**1.4.9版**

**具有備用內容替換的封鎖信號**

作為1.4 TVSDK更新的一部分，Adobe現在還支援針對線性內容進行區域封鎖並從區域封鎖中返回。 TVSDK現在可以並行處理主檔案和備用檔案兩個清單檔案，以便即使在顯示替代程式時也監視封鎖信號。

**1.4.8版**

**視頻心跳庫(VHL)已更新到1.5版**

* 能夠發送帶有視頻啟動或視頻/廣告/章節啟動的元資料作為上下文資料。

* 網路通信量減少 — 心跳平均減少，大小減小。

**1.4.7版**

* **現場個性化支援**

支援Adobe個性化伺服器的內部安裝，以自定義客戶端的個性化請求以轉到其他端點。

* **基於解析度的輸出保護**

DRM策略現在可以根據設備的輸出保護功能指定允許的最高解析度。 比如說， _如果HDCP可用，則允許播放解析度高達1080p的內容；如果HDCP不可用，則允許播放解析度高達480p的內容。_

**1.4.4版**

* **視頻心跳庫(VHL)更新到1.4.1.1版**

   * 添加了將來自其他SDK或玩家的不同分析使用案例與Adobe Analytics視頻軟體包捆綁在一起的功能。
   * 已通過刪除 `trackAdBreakStart` 和 `trackAdBreakComplete` 的雙曲餘切值。 廣告斷點是從 `trackAdStart` 和 `trackAdComplete` 方法調用。
   * 的 `playhead` 跟蹤廣告時不再需要屬性。
   * 已添加對Experience CloudID服務的支援。

* **尼爾森SDK整合**

TVSDK現在支援將mTVR和MDPR ID3信標發送到Nielsen SDK，而不需要任何自定義整合。 為了開始，請下載3.1.2.19 NielseniOS應用軟體開發工具包，並按照《iOS程式設計師指南》中的說明進行操作。

**1.4.0版**

* **具有備用內容替換的封鎖信號**

作為1.4 TVSDK更新的一部分，TVSDK現在還支援針對線性內容進行區域封鎖並返回。 TVSDK現在可以並行處理主檔案和備用檔案兩個清單檔案，以便即使在顯示替代程式時也監視封鎖信號。

* **刪除/更換C3廣告**

現在，無需進行其他準備工作即可將新廣告動態地插入到從C3窗口發出的視頻點播(VOD)資產中。 TVSDK現在提供了一個API來刪除自定義內容範圍並動態插入新廣告。 這種功能強大的新功能在直播期間直播/線性內容播放時也很有用，並且在沒有適當時間清理資產的情況下，立即將其拉下來作為按需內容使用。

## 已解決的問題 {#resolved-issues}

如果解決方法與報告的問題相關聯，則顯示Zendesk引用，例如ZD#xxxxx。

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOSTVSDK 3.13**

* (ZD 42085) — 在CMAF流上播放的問題。

* (ZD-43215) — 在廣告進行中取消播放器時崩潰。

* (ZD 43210) — 啟用WebVTT副標題時，iOSHLS回放將凍結。

**iOSTVSDK 3.12**

* 使用TVSDK foriOS3.10時，在播放15分鐘後，即時流將失敗。

### 已解決以前版本中的問題 {#resolved-issues-previous}

**iOSTVSDK 3.11**

* (ZD#40998)- `isFallbackOnInvalidCreativeEnabled` 導致應用程式崩潰。

* (ZD#41289)- `NSInvalidArgumentException` 用這種方法觀察 `customParams` 導致應用程式崩潰。

**iOSTVSDK 3.10**

(ZD#40943)- TVSDK播放器不發火 `PTMediaPlayerStatusError` 網路不可用時通知。

**iOSTVSDK 3.9**

(ZD#40272)-iOSTVSDK無法播放VTT字幕，出現101001錯誤，導致應用凍結。

**iOSTVSDK 3.8**

* (ZD#40087)-iOS因播放器錯誤導致VOD內容過期而崩潰。

* (ZD#40083)- Pre-Roll廣告不用於直播 `OpportunityGenerator` 玩家出錯。

* (ZD#39828)- `CurrentItem` 屬性缺少nullability批注，當通知中包含的播放器狀態為 `PTMediaPlayerStatusStopped`。

**iOSTVSDK 3.7**

(ZD#38961) — 當將多個內容配置為在PiP中播放時，在一個內容完成播放後，內容無法在「畫中畫(PiP)」窗口中播放。

**iOSTVSDK 3.6**

此版本中沒有新問題。

**iOSTVSDK 3.5**

此版本中沒有新問題。

**版本3.3**

(ZD#37820) — 添加了自定義頭HS-Id、HS-SSAI-TAG的允許清單。

**版本3.2**

* **票證#36588**  — 調用MediaPlayer STOP方法時，會出現播放器崩潰。

對幾個帶字幕的流調用STOP方法時觀察到的固定間歇崩潰。

* **票證#37080**  — 看到清單調用的重複請求。
已修復在播放期間對清單URL所發出的重複請求。 TVSDK現在對每個清單進行一次呼叫。

* **票證#37** - CRS規範化規則失敗，其類型為eq匹配類型。修復了當玩家遇到具有&quot;eq&quot;匹配類型的主機名的上次規範化規則集時，玩家曾崩潰的情況。

**版本3.1**

**票證#36313**  — 在即時流中線性廣告中斷期間，線上性廣告中斷期間，在固定間歇播放期間，出現間歇性不可預知的結果。

**3.0.1版**

**票36948** - CRS — 在iOS12上不一致的資產選擇順序為CRS選擇的資產並不總是在VAST或VMAP響應中返回的最高質量變數。

**版本3.0**

* **票35311**  — 在電話呼叫中斷期間，播放器狀態未變為「已暫停」添加的中斷處理程式以阻止播放器中斷。 中斷時，播放器狀態變為「暫停」，然後按一下播放按鈕繼續播放。

* **票36685**  — 即時資產 — 時間與播放器時間進度和SCTE標籤時間不匹配為SCTE標籤（活動點之前）計算正確時間。

* **票36492** - `currentTime` 和 `localTime` 在暫停狀態期間查找新位置時不更新播放器的當前時間現在可以設定為零，以防播放器處於暫停狀態；較早時，當前時間僅在播放狀態設定為零。

**1.4.45版**

* **票36294** -iOSTVSDK在Xcode 10中不起作用已修復XCode 10上TVSDK的編譯問題。 由於XCode ten要求，iOS1.4.45版以後基於TVSDK構建的應用程式要求最低部署目標為iOS7.0

* **票36321**  — 在可尋的範圍中觀察到的差異 `PTMediaPlayer` 和 `AVPlayer` 實例 _播放_ 狀態。

* **票36493** - `libstdc++` 支援iOS12解決iOS12上TVSDK的匯編問題。 基於iOSTVSDK構建的應用1.4.45以後要求最低部署目標為iOS7.0

**1.4.44版**

* **票34683**  — 廣告播放進度時間為負

當廣告伺服器報告的持續時間與實際廣告內容之間不匹配時，將進行其他檢查以處理此情況。

* **票34801** - `currentTime` 和 `localTime` 在暫停狀態中查找新位置時未更新播放器的當前時間現在可以設定為零，以防播放器處於暫停狀態；較早時，當前時間僅在播放狀態設定為零。

* **票35037**  — 從基於信號的廣告插入返回時，使用錯誤的URL播放停頓。
為1.4.42版中的已關閉問題#34385提供了改進的修復。 已添加isCancelled檢查和異常處理代碼，使操作隊列更加強健。

**1.4.43版**

* (ZD#32990)-iOS:在某些提示點上播放內容，而不是廣告。 `selectedMediaOptionInMediaSelectionGroup` API是AVPlayerItem介面的一部分，現在已移動到 `AVMediaSelection` iOS11號。 使用此新API解決了問題。

* (ZD#33683)已刪除TVSDK `==` 元資料字串的尾碼。 問題在分析邏輯中已解決。

* (ZD#33905)-iOSTVSDK使用兩個用戶代理調用清單檔案。 用戶代理問題已在第一次m3u8呼叫（新安裝案例）中解決。 M3u8的所有呼叫都有相同的用戶代理。

* (ZD#34293) — 在LINEAR流上插入的預輥在iOS11上不能正確播放。 預卷廣告的問題已解決。

* (ZD#34684) — 應用廣告跳過策略時，預滾廣告幀將顯示幾秒鐘。 新的API `enableVodPreroll` 已引入用於在vod播放中禁用預滾動播放。 此API的預設值是 _是_。 該API確保跳過主內容中的廣告內容拼接。

* (ZD#34765) — 呼叫後 `stop()`，仍然下載的傳輸流段很少。 增強 `Stop()` API以避免下載額外段。

* (ZD#34865)- [!DNL Livestream] 截斷在iOS。 與iOS11相關，並添加額外的檢查來確認流是預滾還是主內容，這解決了此問題。

* (ZD#35093) — 修復故障切換方案，其中，如果流的主變數在啟動時失敗（返回404），則回放不會切換到備份流。

**1.4.42 (1.4.42.118)**

* (ZD#34385) — 從基於信號的廣告插入返回時，播放停止，URL錯誤。

   增加的最大併發計數 `CustomAVAssetLoaderOperations`，以便清單讀取繼續執行。

* (ZD#34373) — 當不允許流記錄時，最終用戶無法流到HDMI連接的設備。

* (ZD#32678)- TVSDK未收集iOS上的正確廣告ID。

   如果存在VAST/VMAP重定向，則VHL ping中會接收最終廣告創意的廣告ID。

* (ZD#33904)- TVSDK未註冊用於AVFoundation通知 `AVAudioSessionMediaServicesWereLostNotification` 和 `AVAudioSessionMediaServicesWereResetNotification`。

   `PTMediaServicesWereLostNotification` 和 `PTMediaServicesWereResetNotification` 現在可以在播放器應用程式上註冊，以在媒體服務重置或丟失時獲取通知。

* (ZD#33815) — 客戶無法在不需要應用程式更新的情況下更新其優先順序排序和標準化CRS規則。

   已添加 `getCRSRulesJsonURL` 和 `setCRSRulesJsonURL` iOSTVSDK的API。

**版本1.4.41(1.4.41.76)**

* (ZD #34464) — 使用TVSDK 1.4.41版構建參考應用時出現的問題

   啟動此版本時，為iOS編譯TVSDK需要Xcode 9。
* (ZD #29456) — 播放在暫停狀態中開始

   已修復進入播放時視頻暫停時的暫停問題。
* (ZD #30371) — 當我們線上性流中插入兩個以上廣告時，AdBreak開始時間將發生變化

   已修復嘗試在Apple電視上播放內容時的錯誤，這會完全阻止播放
* (ZD #32146) — 否 `PTMediaPlayerStatusError` 在阻止iOS11開發測試版上接收HLS Live內容

   否 `PTMediaPlayerStatusError` 在使用Charles（Drop connection和403）阻塞時接收HLS Live和VOD內容。

* (ZD #29242) — 啟用廣告後播放視頻播放失敗。

   當廣告啟用和AirPlay啟用開始播放視頻時，視頻播放從不啟動，不會顯示錯誤。

* (ZD#33341)- `DRMInterface.h` 觸發Xcode 9中的生成警告。

   在中固定兩個塊原型 `DRMInterface.h` 在參數清單中缺少&quot;void&quot;一詞。

* (ZD#31979) — 當iOS10或更高版本用於iPhone7/iPhone7+時不編譯/運行。

   不再支援iOS7之前的固定編譯IB文檔。

* (ZD#32920) — 廣告分段內的空白螢幕，沒有廣告分段完成。

   當廣告斷點顯示廣告實例時，在廣告實例完成後，將顯示空白螢幕。

* (ZD#32509) — 禁用iOS11螢幕錄制禁用iOS11上的螢幕錄制。

* (ZD#33179)-iOS11上的間歇性事件故障。

   已修復iOS11上的事件失敗。

**1.4.40版** (1.4.40.72)

* (ZD #32465) — 播放器無法處理合併的播放清單。

   呼叫 `finishLoadingWithError`(與：錯誤)，用於嘗試備用流/觸發故障切換。

* (ZD #31951) — 許可證輪轉期間出現TVSDK錯誤。

   已修復許可證輪換問題。
* (ZD #31951) — 廣告分段內的空白螢幕，沒有廣告分段完成。

   處理了FacebookVPAID廣告通常在單個塊中返回多個CDATA塊的問題 `<AdParameters>` VAST節點。
* (ZD #33336)-iOSTVSDK - Ad pods未被填充，儘管Freewheel已返回足夠多的廣告。

   在序列和回退廣告之間建立父子關係，並根據父序列和索引進行排序。

**1.4.39版** (1.4.39.43)

* (ZD #32178)-iOSTVSDK版本不正確。

   日誌檔案中的TVSDK版本輸出為1.0.211。它已修復，以輸出正確的版本。

* (ZD #32199) — 懶惰廣告載入 — 不顯示內容的視頻。

   以前未初始化的本地Adbreak時間線現在在使用前刷新。

* (ZD #27528) — 如果在iOS1.2上將輔助音頻設定為非預設值，則在資產開始播放後1-45秒，視頻、音頻或兩者都凍結。

   準備並通知處於「就緒」狀態的音頻軌道。

* (ZD #30411) — 如果您選擇輔助Sap語言，則可能會獲得意外結果，如沒有音頻或不正確的音頻。

   準備並通知處於「就緒」狀態的音頻軌道。

* (ZD #32199) — 懶惰廣告載入 — 不顯示內容的視頻。

   以前未初始化的本地Adbreak時間線現在在使用前刷新。

* (ZD #27528) — 如果在iOS1.2上將輔助音頻設定為非預設值，則在資產開始播放後1-45秒，視頻、音頻或兩者都凍結。

   準備並通知處於「就緒」狀態的音頻軌道。

* (ZD #30411) — 如果您選擇輔助Sap語言，則可能會獲得意外結果，如沒有音頻或不正確的音頻。

   準備並通知處於「就緒」狀態的音頻軌道。

**1.4.38版** (1.4.38.860)

* (ZD #29281)-iOS:向CRS請求添加AdSystem和Creative Id

基於CRS規範化規則的CRS請求中創造性ID和AdSystem的使用

* (ZD #29176)- `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

現在已處理由於空AdBreak而導致的崩潰。

* (ZD #30125) — 方案廣告在iOS平台中不起作用

在iOS增加了方案廣告支援。

* (ZD #30782)- #EXT-X-PROGRAM-DATE-TIME通知

沒有為# EXT-X-PROGRAM-DATE-TIME標籤觸發帶有LIVE DRM流的定時元資料事件。

**版本1.4.37(1.4.37.842)**

* (ZD #28950)- VOD播放問題

當流中的# EXT-X-PLAYLIST-TYPE標籤設定為「事件」而不是VOD時，播放問題

* (ZD #29281)-iOS:向CRS請求添加AdSystem和Creative Id

基於CRS規範化規則的CRS請求中Creative Id和AdSystem的使用

* (ZD #29462)- A&amp;E VOD中的TuchHub廣告導致iOS應用崩潰

**版本1.4.36(1.4.36.835)**

* (ZD #29418) — 持續時間為0(#EXT-X-CUE-OUT:0.000)的提示正導致iOSTVSDK停止或崩潰回放。

問題已解決，並且播放正確啟動。

* (ZD #29462) — 視頻點播中的廣告導致iOSTVSDK崩潰。

問題已解決。 iOSTVSDK正在 `exception(AUDNetworkAdInfo::initWithAdId)` 而不是處理。 異常是由於空廣告ID。

* (ZD #29281) — 向CRS請求添加AdSystem和Creative ID。

在1401和1403請求中將AdSystem和CreativeId作為新參數（所有其他參數保持不變）。

**1.4.35版** (1.4.35.830)

* (ZD #27830) — 需要以寫程式方式確定iOS的隱藏字幕和字幕之間的差異。

TVSDK現在顯示兩種類型，這兩種類型可用於過濾所需的標題類型。

* (ZD #29160) — 在TVSDKiOS上，EXT-X-CUE-OUT廣告提示未正確拼接。

EXT-X-CUE-OUT微道廣告正在播放。

* (ZD #29100) — 當用戶掃描到影片結尾時，應用崩潰。

已修復與同步相關的多個崩潰。

* (ZD #28785),(ZD #27712)和(ZD #25076)-iOS應用在大型現場活動中崩潰。

已修復與同步相關的多個崩潰。

**1.4.34版** (1.4.34.815代表iOS6.0+)

* (ZD #28481) — 由於在這些FER流的廣告中斷結束時附加了不正確的密鑰，導致FER中斷

對於FER流，在廣告中斷結束後插入廣告中斷之前的密鑰。 此問題通過附加 *上次查看的密鑰* 廣告結尾。

**1.4.33版** (1.4.33.803代表iOS6.0+)

* (ZD# 21701)為子帳戶啟用CRS

根據CRS後端的要求，通過發送1401 CRS請求的原始建立URL而不是標準化URL來啟用。

* (ZD# 26218)- `PSDKResources.bundle` 載入問題

通過更新資源載入以從所有可用捆綁包中查找，解決此問題。

* (ZD# 27460)Midroll第一個廣告呼叫 — POST至 `cdn.auditude.com` 返回403。

新CDN帳戶無法處理POSTCDN請求。 此問題已通過更新代碼來解決 `cdn.auditude.com` 要求成為GET而不是POST。

**1.4.32版** (1.4.32.792代表iOS6.0+)

* (ZD# 27132)支援VMAP廣告分段的小數值。

當內容未按定義的廣告分段進行分段時，整數會導致意外的廣告放置。 未將十進位值轉換為整數，從而解決了該問題。

* (ZD# 27189)帶有EXT-X — 不連續序列標籤的AES內容未正確播放。

通過將標籤置於播放清單的開頭，解決了此問題。

**1.4.31版** (1.4.31.785代表iOS6.0+)

* (ZD# 24528)實施TVSDK計費使用度量

有關詳細資訊，請參見 [計費度量]。

* (ZD# 24642)對TVSDK的畫中畫支援

「畫中畫」功能已修復，但有時無法正常工作。

* (ZD# 25246)錯誤廣告中斷信號

通過跨變型艙單對齊不連續標籤解決了這一問題。

* (ZD# 26218)當嘗試包括 `PSDKLibrary.framework` 在客戶端的應用程式框架中

此問題通過打包 `PSDKLibrary.framework` 按要求。

* (ZD# 26364)對CRS廣告的多CDN支援

有關詳細資訊，請參閱CRS廣告交付的多個CDN支援。

* (ZD# 27028)在iOS10中延遲播放某些流。

通過為沒有M3U8擴展的流提供一種解決方法，此問題得到解決。

**1.4.30版** (1.4.30.754代表iOS6.0+)

已在此版本中為TVSDK解決了以下問題：

* (ZD# 24180)向允許清單添加自定義標頭。

新的自定義頭已添加到TVSDK允許清單。

* (ZD# 25016)設定ABR控制參數時，會隨機選擇故障轉移流

通過將ABR流維護為與 `initialBitrate` 在包含故障轉移URL的流上進行設定。 這樣可避免播放故障轉移流而不是主資料流。

* (ZD# 25076) `PTAuditudeAdResolver loadComplete`

已解決在快速啟動/停止多個帶廣告的PTMediaPlayer實例期間發生崩潰的問題。

* (ZD# 25960)沒有附加訂閱的標籤用於觸發元資料更改通知廣播

當訂閱標籤出現在清單中的第一段之前時，未通知其的問題。

* (ZD# 26084)PSDK拋出106000.101000.-11833解碼器在從上次廣告中斷轉換回娛樂內容時未發現錯誤

當VMAP的最後一個廣告中斷開始時間在總持續時間完成之前落後時，在某些情況下，直到最後一個廣告中斷結束之後才插入密鑰。 此問題已解決。

* 視頻心跳庫(VHL)已更新到1.5.9版，以解決以下問題：

* (ZD #22351)VHL — 分析：即時視頻資產持續時間

通過添加  `assetDuration`  API到 `PTVideoAnalyticsTrackingMetadata` 更新即時/線性流的資產持續時間，並提供用於檢查即時流的邏輯。

* (ZD# 22675)VHL — 分析：正在更新即時視頻資產持續時間

此問題與ZD #22351相同。

* (ZD #25908)VHL — 分析：Adobe心跳事件崩潰

通過更新實施，使用iOS1.5.9版的VHL最新版本來改善穩定性和效能，解決了這一問題。

* (ZD #25956)VHL — 分析：反複播放視頻時崩潰

此問題與ZD #25908相同。

**1.4.29版** (1.4.29.743)

* (ZD# 23901)第三方廣告未播放

通過切換到CRS v3 URL結構，將區域ID包括在重新打包的URL中，解決此問題。

* (ZD #25183)在tvOS和iOS上播放DRM的問題

通過支援多DRM支援所需的多個密鑰標籤，解決了此問題。

* (ZD# 25334)TVSDK無法播放cDVR共用內容

通過阻止TVSDK將空字串轉換為絕對URL，解決此問題。

* (ZD# 25347)在AVURLAsset上設定自定義HTTP標頭

通過支援 `PTNetworkConfiguration` 已添加類。

**1.4.28版** (1.4.28.722)

* (ZD #24549)多個廣告跟蹤呼叫

通過更新時間線管理器以在建立多個玩家時偵聽特定對象上的通知，解決此問題。

* (ZD #24758) `PTManifestLogger` 不支援iOS8

通過將記錄器實用程式庫更新到7.0版部署目標來解決此問題。

* (ZD #24775)由於廣告而延遲流

通過正確計算事件播放清單上的持續時間漂移，解決了此問題。

* (ZD #24799)有些劇集沒有在iOSAPP上播放

當WebVTT檔案受地域限制時，使用本地Web伺服器進行字幕解決了此問題。

**1.4.27版** (1.4.27.711)iOS6.0+

* (ZD #24089) — 針對長DVR流進行優化和解析

通過添加多個優化來減少在即時/線性流中處理DVR窗口所需的時間，解決了此問題。

* (ZD #21554) — 未為 `application-type = video/mp4`

通過使播放器能夠ping無效資產格式上的正確錯誤跟蹤URL來解決此問題。

* (ZD #24424) — 類型崩潰 `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` 源於內部 `PSDKLib` 用於更新的硬體設備上。

由於取消分配的媒體播放器實例而發生的崩潰（當播放在不同流之間快速切換時）已被修復。

* (ZD #24575) — 在32位設備上發生崩潰 `enableDebugLog=true`

啟用日誌記錄時導致32位設備崩潰的日誌格式問題已解決。

**1.4.26版** (1.4.26.702)iOS6.0+

* (ZD# 20213) — 對於XCode7, TVSDK FW必須是動態/模組化的

通過更新具有模組支援的庫來修復

**1.4.25版** (1.4.25.684)iOS6.0+

* (ZD #19629) — 進入ATV 4播放時即時視頻暫停

此問題已通過在刪除舊項目後但在將新項目添加到 `AVQueuePlayer`。 如果沒有等待期，則通知會發送到不正確的項。

* (ZD #19856) — 預設啟用時不顯示字幕

Webvt播放清單中導致字幕無法正確顯示的問題已得到解決。

* (ZD #21590) — 最新原始生成中的視頻效能和跟蹤

中缺少視頻長度的問題 `VideoAnalytics` 已修復。

* (ZD #20202) — 設定自定義字幕樣式會使iOS應用崩潰

通過在設定字幕樣式時添加其他空對象檢查，解決此問題。

* (ZD #20709) — 視頻開始跟蹤中報告為0的視頻長度

此問題與(ZD #21590)相同。

* (ZD #22280) — 分析視頻長度設定為0

此問題與(ZD #21590)相同。

* (ZD #22592) — 黃金時段Airplay問題

此問題與(ZD #19629)相同。

* (ZD#22922) — 用於iOS的手動比特率切換

通過提供指定最大比特率的選項解決了此問題。

* (ZD #23084) — 僅IPv6網路的Apple合規性

已刪除Apple不推薦用於IPv6相容性的符號。

**1.4.24版** (1.4.24.661)iOS6.0+

* ZD #2548) — 黃金時段支援移動互動式廣告 — VPAID 2.0

如果VPAID廣告無法播放，則通過更新邏輯來取消隱藏播放器視圖來解決此問題。

* (ZD #20101) — 在廣告回放期間，自定義章實現將觸發章節啟動事件

此問題已通過更新解決 `VideoAnalyticsTracker` 在章節和非章節邊界之間轉換時正確檢測章節的開始/完成。

* (ZD #20784) — 分析：觸發內容完成即時視頻轉換

通過添加邏輯來在視頻跟蹤會話期間手動觸發內容完成，解決了此問題。

已更新以下庫：

* AdobeMobile庫到4.10.0
* VHL庫到1.5.6
* VHL-Nielsen圖書館至1.6.7
* (ZD #21855) — 在中盤後不播放字幕

在本期中，重複的不連續性標籤導致字幕在中間卷之後不出現。 通過刪除彼此相鄰的不連續標籤解決了此問題。

* (ZD #21994) — 中的字串超界 `PTHLSUtils`

崩潰的最可能原因是EXT-X-KEY的URL被引號包圍。

* ZD #22074)- `AUDVAST` iOS每分鐘發生一次車禍

在1.4.23版中，由於VAST重定向URL中存在不安全字元而導致的崩潰已修復。 不過TVSDK還是在跳過這些廣告。

通過處理不安全字元和允許播放廣告來解決此問題。

* (ZD #22694)- `PTMediaPlayer`。  視圖由播放器隱藏

如果VPAID廣告無法播放，則通過更新邏輯來取消隱藏播放器視圖來解決此問題。

**1.4.23版** (1.4.23.641)iOS6.0+

* (ZD #18016) — 黃金時段SDK沒有發出網路狀況不良的響應

通過改進錯誤通知，解決了此問題 `AVFoundation` 執行，並允許應用在錯誤後處理重新啟動。

* (ZD #20580) — 發生車禍 `PTSplicerManager`

此問題通過提供額外保護來解決導致崩潰的併發問題。

* (ZD #21782)-iOS錯誤代碼10100

TVSDK在Adobe訪問DRM流上開始播放時返回101000錯誤的問題已解決。

* (ZD #21889) — 線上廣告和離線內容回放失敗

在AES加密離線內容上的廣告修復後播放失敗的問題。

* (ZD #22074)- AUDVAST Crash每分鐘在iOS發生一次

通過改進對URL中具有無效字元的第三方VAST廣告標籤的處理，解決此問題。

* (ZD #22257)- TVSDK無法回放DRM流

在Adobe訪問DRM流上開始播放時返回101000錯誤的TVSDK已修復問題。

**1.4.22版** (1.4.22.627)iOS6.0+

* (ZD #18709)-iOSTVSDK崩潰

已解決某些Adobe訪問DRM保護流上發生崩潰的問題。

* (ZD #18850) — 根據CRS規則更新創造性選擇邏輯

通過添加.json配置檔案來指定創作選擇優先順序，解決此問題。

* (ZD #19770) — 受保護的AES視頻源不再播放

某些302個重定向流無法播放的問題已解決。

* (ZD #19629) — 進入ATV 4播放時即時視頻暫停

通過為AppleTV 4設備開啟播放時添加即時視頻暫停的解決方法，解決此問題。 問題似乎是AppleTV 4問題。

* (ZD #21119) — 廣告播放後TVSDK將停止

在使用廣告插入時，已添加了對序列IV的AES加密流的支援。

* (ZD #21125) — 提前從即時/線性廣告返回

已添加支援，以便在播放廣告前提前從廣告中斷返回到完成。 通過自定義清單標籤指示提前返回。

* (ZD #21224)- Akamai對標籤流的空中支援

API已添加到 `PTNetworkConfiguration` 類，用於在某些Akamai標籤流的段上附加cookie作為URL參數。

* (ZD #21287) — 無關日誌

xcode控制台中預設顯示的某些日誌語句的問題已得到解決，即使日誌記錄處於禁用狀態也是如此。

* (ZD #21446)- Ad Break事件有時不由TVSDK觸發

在EVENT流上，在先前版本生成中未正確觸發廣告中斷。 此生成解決了此問題。

**1.4.21版** (1.4.21.605)iOS6.0+

* (ZD #20749) — 回退跳過非空VAST響應；附加廣告跟蹤URL觸發

已解決回退廣告上重複ping的問題。

**1.4.20版** (1.4.20.590)iOS6.0+

* (ZD #18639)- TVSDK在長時間的熱錄制資產上使用過多的CPU/資源

CPU/資源使用量過高已在兩個級別中固定。 首先，讓時間更新函式在全局隊列上運行，而不是主線程上運行，並通過優化CPU使用率，以用先前處理和快取的m3u8分析清單。

* (ZD #19349) — 限制網路連接時跳過預滾廣告。

通過向應用程式和 `adMetadata.adRequestTimeout` API，以覆蓋預設的10秒超時。

* (ZD #19446) — 即時流上缺少通知

通過允許應用程式訂閱 `EXT-X-PROGRAM-DATE-TIME` 在直播流上。

* (ZD #19459) — 準備備用音頻時崩潰 `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) — 崩潰 —  `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

此問題與Zendesk #19459相同。

* (ZD #19574)- TVSDK不返回DRM或非DRM內容的M3U8響應資料

在清單檔案的初始載入中 `PTMediaPlayerItem.prepareToPlay`，如果載入清單失敗，則TVSDK不會向應用程式報告失敗響應的正文。

通過允許TVSDK將故障響應報告為應用程式錯誤，解決此問題。

* (ZD #19615) — 回退邏輯不工作

在當前實施中，回退廣告被跳過，除非這些廣告採用m3u8格式，否則不會重新打包。 此問題通過添加對重新打包回退廣告的支援而解決。

* (ZD #19770)- TVSDK無法播放任何帶302重定向的受保護AES內容

重定向問題已解決，因為重定向URL被刪除 `cleanConnectionData` 才能用於分析清單。

* (ZD #19856) — 預設啟用時，某些位速率不顯示字幕

通過處理未顯示字幕的流段的iOS錯誤，解決了此問題。

* (ZD #19868) — 當無效的創作工具被販運時，TVSDK崩潰

TVSDK中錯誤地取消分配大型分析器實例的崩潰已修復。

* (ZD #20180)- VPAID廣告偶爾被跳過

JavaScript mime類型並不總是包含或視為有效的mime類型。 通過將JavaScript作為有效的MIME類型來解決此問題。

* (ZD #20749) — 回退跳過非空VAST響應；附加廣告跟蹤URL觸發

一些創意人士沒有重新包裝的問題已經解決。

**1.4.19版** (1.4.19.563)iOS6.0+

* ZD #18639)- TVSDK對冗長的熱錄制資產使用過多的CPU/資源

通過優化DRM m3u8播放清單重寫到先前已重寫的播放清單的快取位，解決了此問題。 這在您回放每段下載後下載的即時m3u8流時最為相關。

* (ZD#18956)- `player.drmManager` 在iOS演示播放器中設定斷點時為零

通過更新 `PTMediaPlayer.drmManager` API實現，從DRM框架中選取DRManager。

**1.4.18版** (1.4.18.557)iOS6.0+

* (ZD #18844)在iOS播放器中跟蹤即時內容的播放頭。

通過允許應用程式設定其自己的播放頭值，解決了此問題。

* (Zendesk #18518) — 如果未指定視頻名稱，則TVSDK的名稱預設為基於* PSDK的播放器。*

通過刪除播放器名稱的預設值解決了此問題。

**1.4.17版** (1.4.17.545)iOS6.0+

* (Zendesk #2228) — 增強TVSDK以返回清單提取的JSON響應

當內容不是M3U8時，DRM框架不會發送錯誤，而是返回零DRMetadata。 在M3U8_PARSER_ERROR通知發生時，通過添加元資料來公開內容，解決了該問題。

* (Zendesk #2231) — 從獲取MediaPlayerNotification中不可用的清單返回錯誤

與Zendesk #2228相同的解析度

* (Zendesk #3304)- VAST 3.0 `[ERRORCODE]` 未填充宏

問題 [!DNL Auditude] 當已解析跟蹤URL開頭有空格時，SDK無法發送ping。

* (Zendesk #17294) — 崩潰 [!DNL SecKeyRawSign]

已解決當客戶代碼使用密鑰鏈時可能發生的崩潰。

* (Zendesk #18008) — 支援Cookie，支援iOS8+，以支援標籤化流

Akamai標籤化流要求根據段請求發送Cookie，而在iOS7和更早的版本上是不可能的。 從iOS8號開始，Apple公司增加了一個API，允許為段請求傳遞cookie。 TVSDK中現在提供了此支援。 還添加了對發送用戶代理的支援（如果可用）。

* (Zendesk #18166)- TVSDK 1.4.15在使用 `DWARF` 與 `dSYM` 檔案選項

所有警告都已解決。

**注釋**:已為TVSDK添加了與OS相容的電視庫。

**1.4.16版** (1.4.16.1454)

* Zendesk #3875 — 播放期間Tab S崩潰

恢復OKHTTP對的依賴項 [!DNL Auditude] 因為TVSDK現在直接使用 `httpurlconnection` 而不是捲髮。 通過在進行另一次JNI呼叫前清除異常解決了此問題。

* (Zendesk #4487) — 跟蹤線性內容通道

通過線上性流回放會話期間重新初始化視頻心跳跟蹤器解決了此問題。

* (Zendesk #17919)- Android — 內容查找導致心跳錯誤

問題是當一章中有查找時，解決心跳處於錯誤狀態

* (Zendesk #18053) — 在棉花糖上使用TVSDK崩潰的應用程式

當TVSDK庫使用Neon代碼執行YUV時，TVSDK在Android™ M作業系統上崩潰 `->` RGB顏色轉換。 通過使用非neon版本的 `code`。

* (Zendesk #18072)- Android M — 應用程式崩潰

呼叫時發生此崩潰 `MediaCodecList` 和 `MediaCodecInfo` 檢查是否支援配置檔案和級別時的API。 Adobe正尋求Google的支援，以獲得更多洞察力。 通過提前載入所有編解碼器資訊來提供臨時解決問題，以避免僅在需要編解碼器資訊時才調用這些API。

* (Zendesk #18074) — 阿拉伯文字幕在Nexus上與Android™ 6.0不相容

通過支援Android™ CTS字型映射解決了此問題。

**1.4.15版** (1.4.15.512)iOS6.0+

**注釋**:尼爾森模組已從TVSDK版本中刪除，但TVSDK將很快用新的尼爾森整合模組更新。

* (ZD #2228) — 獲取清單時返回錯誤，該清單在 `MediaPlayerNotification`

添加元資料以在通知時公開內容 `M3U8_PARSER_ERROR` 。

* (ZD #4437)-Adobe PrimetimeSDK內崩潰

已修復在準備字幕/備用音頻時報告的故障。

* (ZD #4487) — 跟蹤內容的線性通道

允許線上性流回放會話期間重新初始化視頻心跳跟蹤器。

**1.4.14版** (1.4.14.498)iOS6.0+

* (ZD #17260)- `playlistManagerForURL`

已修復由於併發問題而導致的間歇性崩潰。

**1.4.13版** (iOS6.0+)

* (ZD #3304)- VAST 3.0 `[ERRORCODE]` 未填充宏

   * 如果內聯廣告的創作性不好，則會顯示錯誤代碼400。
   * `[ERRORCODE]` 宏是URL編碼的。

* (ZD #3865)心跳與IMA廣告整合

修復了錯誤報告視頻長度的錯誤。

* 更新TVSDK演示播放器以支援iOS9

要正確支援iOS9，必須配置應用程式運輸安全性的例外。 對於演示，ATS完全禁用。

**1.4.12版** (1.4.12.464)iOS6.0+

* (ZD #4521)CRS測試客戶端和SSAI

已修復3P URL中不正確的反向MD5。

**1.4.12版** (1.4.12.463)iOS6.0+

* (ZD #2751)CSAI和CRS/增強：處理某些媒體檔案URL中的動態元素。

更新的Creative Repackaging Service以正確處理使用動態Creative URL的廣告。

* (ZD #3654)1.3.4.166後PSDK版本中的記憶體洩漏

固定記憶體洩漏 `drmFramework` 在iOS8.2設備上定期播放

* (ZD #3988)在首次播放後重新查找到前滾時將跳過前滾

已修復錯誤，以便可以正確禁用廣告策略。

* (ZD #4017)請求iOSAPI在反向尋道時強制和回放

已解決ZD #4279的修復

* (ZD #4279)HLS TVSDK廣告插入 — iOS和案頭上的重定向問題

修復Ad資產使用相對重定向URL時的錯誤

**1.4.9版** (1.4.9.427)iOS6.0+

* (ZD #3075)網際網路可接通性問題 — iOS

已添加通知以檢測播放何時停止。

* (ZD #3193)在TVSDK中請求配置檔案更改API

已更新 `PTPlaybackInformation` 顯示更新的指示位速率。 已更新 `BITRATE_CHANGE` 通知M3U8報告的比特率更可靠和準確。

* (ZD #3324)VMAP無廣告媒體時黃金時段廣告報告問題

支援ping空廣告中斷跟蹤URL,TVSDK現在驗證廣告中斷開始並完成ping空廣告中斷。

**1.4.8版** (1.4.8.402)

* (ZD #3158)IOS7起全事件重放事故

**1.4.7版** (1.4.7.382)

* (ZD #2197)跟蹤和錯誤。 為資產添加的通知無法載入清單。
* (ZD #2894)播放器在回放期間發出四個頂級清單請求。
* (ZD #2992) [!DNL Auditude] 報告奇怪的持續時間和標識符。

**1.4.6版**(1.4.6.325)

* (ZD #2197)跟蹤和錯誤。 為資產添加的通知無法載入清單

**1.4.5版** (1.4.5.283)

* (ZD #2141) [!DNL TreeHouse] 應用程式，已添加 `AdobeAnalyticsPlugin.a` 庫以生成包。
* 視頻心跳庫更新到1.4.1.2
* (PTPALY-4226)(與ZD #2423相關)執行DRM重置可導致刪除應用程式文檔資料。

**1.4.4版** (1.4.4.242)

* 視頻心跳庫(VHL)更新為1.4.1。

* (ZD #2435)分析需要更新的TV SDK文檔

**1.4.2版** (1.4.2.210)iOS6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` 返回空
* (ZD #2109)黃金時段PSDK 1.4.1.125與Xcode不工5.1.1
* (ZD #2137)無法載入DRM元資料時在iOS的PSDK中崩潰

**1.4.1版**(1.4.1.125)

* (ZD #1107) [!DNL CocoaLumberjack] 重複符號
* (ZD #1644)修改iOS用戶代理以進行目標和報告
* (ZD #1850)iOSSDK中包含的Cocoa Lumberjack檔案
* (ZD#1908)如果自定義標籤超過1個，PSDK將忽略自定義標籤

**1.4.0版** (1.4.0.32)

* Zendesk #1024 — 通過清單從流中刪除廣告的功能

## 設備認證和支援 {#device-certification-and-support}

>[!NOTE]
>
>以下功能包括 **不** TVSDK中支援：
>
>* 在任何平台或版本上執行慢動作。
>* 真人秀。


**1.4.43版**

* TVSDK 1.4.43經iOS11認證。

**1.4.29版**

* TVSDK 1.4.29已通過iOS10認證。

**1.4.28版**

* TVSDK 1.4.28已通過iOS10 Beta 7認證。
* 通過添加HTTPS強制使用DRM支援  `forceHTTPS`  和 `isForcingHTTPS` API。
* 已將VHL庫更新為1.5.8，將Mobile庫Adobe為4.8.4，並將記錄器實用程式庫更新為7.0版部署目標。

**1.4.19版**

此版本的TVSDK已通過iOS和電視OS的公平播放支援認證。

**1.4.17版**

* 電視作業系統

   此版本的TVSDK包括對tvOS的支援，並且已經為未加密的HLS流進行了認證。

   **注釋**:請記住以下編譯准則：

   * TVSDK tvOs支援限於非AdobeDRM加密流。 必須刪除引用 `drmNativeInterface.framework` 在tvOS生成設定中。 仍支援AES加密流。
   * Apple要求啟用所有Apple電視應用程式的位碼，因此必須在項目設定中開啟此標誌。

## 已知問題和限制 {#known-issues-and-limitations}

* 由於iOSUIWebView類被棄用，在iOSTVSDK 3.6以後：
   * VPAID廣告在iPad13號不如預期播放。
   * 伴侶廣告沒有按預期播放。

* 在iOSTVSDK，所有廣告都被縫入內容清單。 廣告行為通過基於內容和廣告片段的持續時間的搜索來實現。 因此，如果段持續時間不準確，則搜索可能並不總是以廣告中斷開始或結束的準確幀結束。 即使持續時間與幀相關，平台本身也具有對查找的容限，並且可能顯示一些幀或廣告或內容。 這是平台的局限性，也是廣告插入與iOSTVSDK的協作方式。
* 在這種情況下，在查找事件上會發生跳過的決定。 但是，由於清單中的廣告段持續時間不準確地表示廣告的實際持續時間，所以搜索不是幀精確。 因此，應用廣告策略時，您會看到幾個廣告幀。
* 它可能會體驗到，許可證輪換視頻在iOS11上不會播放，在iOS9.x和iOS10.x上也會播放正常。
* 在VPAID 2.0支援中，如果播放在AirPlay上處於活動狀態，則跳過VPAID廣告。
* 的 `drmNativeInterface.framework` 當最小目標設定為iOS7（或更高版本）時無法正確連結。
解決方法：顯式指定 `libstdc++.6.dylib` 庫，如下所示：轉到 **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** 添加 `libstdc++.6.dylib`。
* 未插入後滾動廣告以替換API。
* 在廣告分段中查找（不會從中出現）會發出重複的廣告開始和廣告中斷通知
* 設定 `currentTimeUpdateInterval` 沒有任何效果。
注：在某些iOS版本中，作業系統不會載入 `PSDKLibrary.framework` 的下界。 手動複製 `PSDKResources.bundle` 到應用程式的捆綁資源：轉到 **生成階段** 並複製捆綁資源。
* 無法使用Xcode 8或更低版本生成引用應用。 iOSTVSDK 1.4.41版以後，使用Xcode 9進行編譯。
* VPAID廣告不尊重 `delayAdLoadingTolerance` 值。
* 24077 — 對於某些帶字幕的HLS內容，玩家崩潰 _停止_ 或 _重置_ 的雙曲餘切值。
* 如果啟用了「Just in Time Ad Resolving（正時廣告解析）」 ，則「Detailed Error（詳細錯誤通知）」不可用。
* 錯誤通知按廣告解決時間記錄，而不是按廣告順序記錄。
* HEVC支援在此版本中有以下限制
   * 不支援DRM
   * CC(CEA 608/708)支援不可用，因為CMAF不支援它。
   * 4K支援尚未提供。
   * ID3標籤支援不可用，因為CMAF不支援它。
   * 未驗證未混合的Live HEVC流。
   * 未驗證HEVC廣告支援。
* 啟用JIT並將容差設定為10秒，如果存在VMAP > VAST重定向廣告，則第一次出現VAST呼叫。
* 為了使Ad解析超時正常工作，每次在即時流回放期間更新播放清單時，播放器都希望在20秒內找到一個縫合的播放清單。 如果在所述間隔內它沒有接收到縫合播放清單，則引發內部錯誤，並且播放器停止。

## 有用的資源 {#helpful-resources}

* [《 TVSDK 3.4 foriOS程式設計師指南》](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDKiOS3.4 API參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://experienceleague.adobe.com/docs/primetime.html) 的子菜單。
