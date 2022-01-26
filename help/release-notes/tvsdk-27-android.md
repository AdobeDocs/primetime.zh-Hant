---
title: 《 TVSDK 2.7 for Android™發佈說明》
description: TVSDK 2.7 for Android™發行說明描述TVSDK Android™ 2.7中的新增或更改內容、已解決和已知問題以及設備問題
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: d64f0ef2-60a9-43a1-b2f9-44764a570538
source-git-commit: 3891ea44775899c1e0d43c4ac74bbc4b07d7962e
workflow-type: tm+mt
source-wordcount: '4070'
ht-degree: 0%

---

# 《 TVSDK 2.7 for Android™發佈說明》 {#tvsdk-for-android-release-notes}

TVSDK 2.7 for Android™發行說明描述TVSDK Android™ 2.7中的新增或更改內容、已解決和已知問題以及設備問題

## TVSDK Android™ 2.7 {#tvsdk-android}

Android™參考播放器隨Android™ TVSDK一起包含在您的分發示例/目錄中。 隨附的README&lt;.md檔案說明了如何構建參考播放器。

>[!NOTE]
>
>要成功構建參考播放器（如隨發行版一起分發的README.md中所述），請確保執行以下操作：
>
>1. 從下載VideoHeartbate.jar [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (適用於Android™ v2.0.0的VideoHeartbat庫)
>1. 將VideoHeartbate.jar解壓到libs/資料夾中。

>


## 新功能 {#new-features}

用於Android™的TVSDK 2.7包含1.4版的所有功能，但下面列出的不支援的功能除外 [特徵矩陣](#feature-matrix)。

**Android™ TVSDK 2.7**

* **並行廣告解決支援**

TVSDK 2.7支援在Ad中斷中並行解析所有Ad請求，而不是順序解析。

### 以前版本中的新功能 {#new-features-previous-releases}

**2.5.6版**

* **TVSDK 2.5支援Android™ P**
* **啟用後台音頻**

   要在應用程式從前台移動到後台時啟用音頻播放，應用程式應在播放器處於PREPARED狀態時調用參數為true的MediaPlayackInBackground API。

* **alwaysUseAudioOutputLatency(boolean val)（在MediaPlayer類中）**

設定後，在音頻時間戳計算中使用輸出延遲。
布爾參數val - True在音頻時間戳計算中使用音頻輸出延遲。

* **已優化，即使頻寬速度突然下降，也能獲得最佳的回放體驗。**
TVSDK現在取消正在進行的段下載（如有必要），並動態切換到相應的格式副本。 這是通過在比特率之間無縫切換而不中斷來實現的。

**2.5.5版**

* **部分Ad-Break插入**

   像電視一樣的體驗，即在廣告中間加入廣告，而不為部分觀看的廣告觸發跟蹤。\
   示例：用戶在90秒廣告中間（40秒）加入，其中包括3個30秒廣告。 這是第二個廣告的10秒。
   * 第二廣告在剩餘持續時間（20秒）後播放第三廣告。
   * 不會觸發播放的部分廣告（第二個廣告）的廣告跟蹤器。 只有第三個廣告的追蹤器被發射。

* **通過HTTPS安全廣告載入**

   Adobe Primetime提供了通過https請求黃金時段廣告伺服器和CRS的首次呼叫的選項。

* **添加到CRS請求的AdSystem和Creative Id**

   * 現在包括 `AdSystem` 和 `CreativeId` 作為1401和1403請求中的新參數。

* **已刪除NetworkConfiguration類中的API setEncodeUrlForTracking** 因為URL中的不安全字元應進行編碼。

**2.5.4版**

Android™ TVSDK v2.5.4提供以下更新和API更改：

* 預設值的更改 `WebViewDebbuging`

   的 `WebViewDebbuging` 值設定為 _假_ 預設值。 要啟用它，請撥打 `setWebContentsDebuggingEnabled` 至 _真_ 的子菜單。

* 已更新OpenSSL和Curl版本升級 `libcurl` 到v7.57.0和OpenSSL到v1.0.2k。
* VAST響應對象的應用級訪問引入了新的API NetworkAdInfo::getVastXml()，該API為應用程式提供了對VAST響應對象的訪問。

**2.5.3版**

Android™ TVSDK v2.5.3提供以下更新和API更改。

* 我們鼓勵所有使用CRS的TVSDK客戶使用TVSDK 2.5.3.85或最新的Android™升級其應用。 這是現有應用程式實現的直接導入替代。 TVSDK升級後，在代理工具中檢查CRS建立URL請求(例如：)，並確認路徑中的主機名和版本與下面的示例URL結構中相同。

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* 可自定義TVSDK的用戶代理：我們添加了一些新API來自定義用戶代理。

   * `setCustomUserAgent`（字串值）
   * `getCustomUserAgent`()

* 在Android™應用程式和TVSDK之間共用Cookie:Android™ TVSDK現在支援在Java™層（儲存在Android™應用程式的CookieStore中）和C++ TVSDK層之間訪問Cookie。 現在，可以設定和/或修改本機C++層中的Cookie，因為它們暴露在Java™ Cookie儲存中。
* API更改：

   * 添加了新的事件CookieUpdatedEvent。 媒體播放器在更新其cookie時將派送它。
   * 將新API添加到 `NetworkConfiguration::set/ getCustomUserAgent()` 使用自定義用戶代理。
   * 將新API添加到 `NetworkConfiguration::set/ getEncodedUrlForTracking` 強制編碼不安全字元。
   * 將新API添加到 `NetworkConfiguration::getNetworkDownVerificationUrl()` 設定網路驗證URL。
   * TextFormat::treatSpaceAsAlphaNum中添加了一個新屬性，該屬性定義在顯示字幕時是否將空格視為字母數字。

* 更改 `SizeAvailableEvent`:以前，為 `SizeAvailableEvent` 在2.5.2中，用於返回由媒體格式返回的幀高和幀寬。 現在，它分別返回由解碼器返回的輸出高度和輸出寬度。
* 「緩衝」行為中的更改：緩衝行為已更改。 如果緩衝區為空，則App Developer需要執行哪些操作。 2.5.3在緩衝區空時使用播放緩衝區大小。

**2.5.2版**

Android™ TVSDK v2.5.2提供了重要的錯誤修復和一些API更改。

**2.5.1版**

Android™ 2.5.1中發佈的重要新功能。

* **效能改進**&#x200B;新的TVSDK 2.5.1體系結構帶來了一些效能改進。 根據來自第三方基準研究的統計資料，新體系結構提供的啟動時間比行業平均水準減少5倍，丟棄幀數減少3.8倍：

   * **即時啟動，用於VOD和即時 —** 啟用即時時，TVSDK會在播放開始前初始化和緩衝媒體。 因為可以在後台同時啟動多個MediaPlayerItemLoader實例，所以可以緩衝多個流。 當用戶更改頻道，並且流已正確緩衝時，新頻道上的播放將立即開始。 TVSDK 2.5.1還支援的「即時開啟」 **活** 流。 當即時窗口移動時，即時流被重新緩衝。

      * **改進的ABR邏輯 —** 新的ABR邏輯基於緩衝區長度、緩衝區長度變化率和測量的頻寬。 這確保ABR在頻寬波動時選擇正確的比特率，還通過監視緩衝器長度變化的速率來優化比特率切換的實際發生次數。
      * **部分段下載/子分段 —** TVSDK進一步減小每個片段的大小，以便盡快開始回放。 ts片段必須每兩秒有一個關鍵幀。
      * **懶惰的廣告解析 —** TVSDK在開始播放之前不等待非預卷廣告的解析，因此減少了啟動時間。 在解決所有廣告之前，仍不允許使用搜索和特技播放等API。 這適用於與CSAI一起使用的VOD流。 在完成廣告解決之前，不允許執行搜索和快速前進等操作。 對於即時流，無法在即時事件期間啟用此功能進行廣告解析。
      * **永久網路連接 —** 此功能允許TVSDK建立和儲存持久網路連接的內部清單。 這些連接可重用於多個請求，而不是為每個網路請求開啟新連接，然後銷毀它。 這提高了網路代碼的效率並減少了延遲，從而加快了回放效能。
當TVSDK開啟連接時，它會要求伺服器 *保持活力* 連接。 某些伺服器可能不支援此類連接，在這種情況下，TVSDK會再次返回為每個請求建立連接。 此外，當持久連接預設處於開啟狀態時，TVSDK現在具有配置選項，以便應用程式可以在需要時關閉永久連接。
      * **並行下載 —** 並行而不是串列下載視頻和音頻會減少啟動延遲。 此功能允許播放HLS Live和VOD檔案，優化來自伺服器的可用頻寬使用，降低進入緩衝區運行不足情況的可能性，並將下載和回放之間的延遲降至最低。
      * **並行廣告下載 —** TVSDK在打斷廣告中斷前平行預取廣告，從而實現廣告和內容的無縫回放。

* **播放**

   * **MP4內容播放 —** MP4短片不需要重新編碼以在TVSDK中回放。
注：MP4播放不支援ABR切換、特技播放、廣告插入、後期音頻綁定和子分段。
   * **帶自適應比特率的特技播放 —** 此功能允許TVSDK在iFrame流之間切換，同時處於特技播放模式。 您可以使用非iFrame配置檔案以較低的速度進行特技播放。
   * **更流暢的特技遊戲 —** 這些改進增強了用戶體驗：

          *在特技播放期間根據頻寬和緩衝區配置檔案進行自適應比特率和幀速率選擇
          *使用主流而不是IDR流，可以快速播放30幀/秒。
      
* **內容保護**

   * **基於解析度的輸出保護 —** 此功能將回放限制與特定解析度相關聯，從而提供更精細的DRM控制項。

* **工作流支援**

   * **直接計費整合 —** 這會將計費指標發送到Adobe Analytics後端，該後端由Adobe Primetime認證為客戶使用的流。
TVSDK自動收集度量，遵守客戶銷售合同，以生成計費所需的定期使用報告。 在每個流啟動事件上，TVSDK使用Adobe Analytics資料插入API將計費度量（如內容類型、啟用廣告插入的標誌和基於可計費流持續時間的啟用drm的標誌）發送到Adobe Analytics黃金時段擁有的報告套件。 這不會干擾或包括在客戶自己的Adobe Analytics報告套件或伺服器呼叫中。 應請求，此開單使用情況報告會定期發送給客戶。 這是僅支援使用計費的計費功能的第一階段。 可以根據銷售合同使用文檔中描述的API進行配置。 預設情況下啟用此功能。 要關閉此功能，請參閱參考播放器示例。
   * **改進的故障切換支援 —** 實施了其他策略以繼續不間斷的回放，儘管主機伺服器、播放清單檔案和段出現故障。

* **廣告**

   * **Moat整合 —** 支援從Moat進行廣告可視性測量。
   * **伴侶橫幅 —** 伴隨條幅顯示線上性廣告旁邊，廣告結束後通常繼續顯示在視圖上。 這些標語可以是html(HTML片段)類型或iframe（iframe頁的URL）類型。

* **分析**

   * **VHL 2.0 -** 這是最新的優化視頻心跳庫(VHL)整合，用於自動收集Adobe Analytics的使用資料。 為了簡化實施，API的複雜性已經降低。 下載VHL庫 [v2.0.0 for Android™](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) 並解壓libs資料夾中的JAR檔案。

* **SizeAvaliableEventListener**
   * getHeight()和getWidth()方法的SizeAvailableEvent現在將分別返回height和width的輸出。 顯示長寬比可計算如下：

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookie**

   * Android™ TVSDK現在支援訪問儲存在Android™應用程式CookieStore中的Java™ Cookie。 當新Cookie作為「Set-Cookie」響應標頭的一部分時，將提供回調API(onCookieUpdated)來記錄。 通過使用CookieStore在該特定URI/域上設定這些Cookie值，這些Cookie作為用於不同URI/域的HttpCookie的清單可用。 同樣，TVSDK中的cookie值會使用CookieStore添加API進行更新。

## 特徵矩陣 {#feature-matrix}

適用於Android™的TVSDK支援各種功能，您可以實施這些功能來向視頻應用程式添加功能。

在下面的功能表中，「Y」表示當前版本支援該功能。

| 功能 | 內容類型 | 合肥光源 |
|---|---|---|
| 常規播放（播放、暫停、查找） | VOD + Live | Y |
| FER — 常規播放（播放、暫停、查找） | FER視頻點播 | Y |
| 在廣告播放時查找 | VOD + Live | 不支援 |
| AC3 | VOD + Live | 不支援 |
| MP3 | 視頻點播 | 不支援 |
| MP4內容播放 | 視頻點播 | Y |
| 自適應比特率切換邏輯 | VOD + Live | Y |
| 僅播放音頻 | VOD + Live | Y |
| 多CDN支援 | VOD + Live | 不支援 |
| 使用純音頻介質播放廣告 | VOD + Live | 不支援 |
| 隱藏字幕 — 608/708 | VOD + Live | Y |
| 隱藏字幕 — WebVTT | VOD + Live | Y |
| 清單故障轉移 | VOD + Live | Y |
| 高級故障切換 | VOD + Live | Y |
| QoS和播放器通知 | VOD + Live | Y |
| 支援Cookie標頭 | VOD + Live | Y |
| 支援自定義HTTP標頭 | VOD + Live | Y（允許列出） |
| 設定緩衝區控制參數 | VOD + Live | Y |
| 設定自適應比特率控制 | VOD + Live | Y |
| 自定義清單標籤 | VOD + Live | Y |
| 後期音頻綁定 | VOD + Live | Y |
| 302重定向 | VOD + Live | Y |
| 帶偏移的回放 | VOD + Live | Y |
| 僅播放音頻 | VOD + Live | Y |
| 特技遊戲 | VOD + Live | Y |
| 《玩技巧的慢動作》 | VOD + Live | 不支援 |
| 平滑特技播放（帶ABR） | VOD + Live | Y |
| ID3分析 | VOD + Live | Y |
| 廣告封鎖 | VOD + Live | 不支援 |
| 即時開啟 | VOD + Live | 不支援 |
| 不連續標籤支援 | VOD + Live | Y |
| 302重定向粘性 | VOD + Live | Y |

| 功能 | 內容類型 | 合肥光源 |
|---|---|---|
| 常規播放，啟用廣告 | VOD + Live | Y |
| 啟用廣告的FER內容 | 視頻點播 | Y |
| 預設廣告行為 | VOD + Live | Y |
| 廣2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4廣告 | VOD + Live | Y（來自CRS） |
| 啟用廣告的特技播放 | VOD + Live | Y |
| 僅廣告 | 視頻點播 | Y |
| 目標參數 | VOD + Live | Y |
| 自定義參數 | VOD + Live | Y |
| 自定義廣告行為 | VOD + Live | Y |
| 自定義廣告標籤 | 實況 | Y |
| 自定義廣告解析器 | VOD + Live | Y |
| 自由輪自定義Ad解析器 | 視頻點播 | Y |
| C3 | VOD + Live | 不支援 |
| 懶惰廣告解決 | 視頻點播 | Y |
| 不連續標籤支援 — SSAI | VOD + Live | Y |
| 夥伴廣告、橫幅廣告和可點擊廣告 | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y(JS) |
| 早期廣告退出 | 實況 | Y |
| 基於規則的創意優先 | VOD + Live | Y |
| CRS規則 | VOD + Live | Y |
| JSON Ad解析器 | VOD + Live | 不支援 |
| Moat整合 | VOD + Live | Y |

| 功能 | 內容類型 | 合肥光源 |
|---|---|---|
| AES加密 | VOD + Live | Y |
| 示例AES加密 | VOD + Live | Y |
| 標籤化流 | VOD + Live | Y |
| DRM | VOD + Live | 僅限黃金時段DRM(未來：維德文) |
| 外部播放(RBOP) | VOD + Live | 僅限黃金時段DRM |
| 許可證輪換 | VOD + Live | 僅限黃金時段DRM |
| 密鑰輪替 | VOD + Live | 僅限黃金時段DRM |

| 功能 | 內容類型 | 合肥光源 |
|---|---|---|
| Adobe AnalyticsVHL整合 | VOD + Live | Y |
| 計費 | VOD + Live | Y |

## 已解決的問題 {#resolved-issues}

如果解決方法與報告的問題關聯，則顯示Zendesk引用，例如ZD#xxxxx

**Android™ TVSDK 2.7**

本節提供TVSDK 2.7版中解決的問題的摘要。

* ZD#37166 — 即使廣告播放正常，錯誤跟蹤呼叫也會被觸發。
* ZD#37134 — 返回錯誤的廣告ID，以防VMAP響應中出現包裝(3P)廣告與多個廣告一起出現。

**Android™ TVSDK 2.5.6**

* ZD #34992 — 隱藏標題中的語言為空。
   * 已修復TVSDK未從主清單分析#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS的案例，以獲取字幕軌道詳細資訊。
* ZD #35078 - Android P驗證。
   * TVSDK 2.5.6已通過最新Android™ P測試版版本的驗證。 由於新的Android™作業系統，未發現問題。
* ZD #34149 — 即使遇到錯誤，播放器仍繼續請求清單。
   * 已修復TVSDK重複調用的情況，即使所有配置檔案都關閉（404錯誤）。
* ZD #31533 — 在應用發送到後台後，在Android™上播放音頻。
   * 已添加 `enableAudioPlaybackInBackground` 應使用「True」作為參數（當播放器處於PREPARED狀態時）調用的MediaPlayer的API，以在應用處於後台時啟用音頻的回放。

**Android™ TVSDK 2.5.5**

* ZD #21647 — 當實際視頻大小為640x360時，Android TVSDK會通知640x368。
   * 由於可變m_nOutputHeight（在AndroidMCVideoDecoder內部）正在使用幀高度而不是實際輸出高度進行更新。 對函式getVideoFrame進行了相關更改，以正確計算m_nOutputHeight。
* ZD #26614 — 緊急 — 第三方廣告服務/方案 — 未能服務印象。
   * 通過處理XML分析中的案例來增強早期的修復，在XML分析中，當「space」位於「equal」符號之前(如 &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android:向CRS請求添加AdSystem和Creative ID。
   * 現在，在1401和1403請求中將「AdSystem」和「CreativeId」作為新參數。
* ZD #33062 - TVSDK在CDATA節點下的VAST響應中發生管道字元時崩潰
   * NetworkConfiguration類中的API setEncodeUrlForTracking作為要編碼的URL中的不安全字元被刪除。
* ZD #33063 - CRS檔案選擇邏輯已中斷 — TVSDK沒有發送CRS的webm格式請求，而是發送3gpp檔案。
   * 已修復邏輯。 在使用webm和3gpp格式的媒體檔案時，CRS請求為webm發送。 並且，在使用3gpp格式的媒體檔案時，CRS請求為最高比特率的3gpp檔案發送。
* ZD #33125 - Android應用在VMAP中使用特定的DoubleClick標籤崩潰。
   * 已修複方案以避免崩潰。
* ZD #32256 — 許可證輪替和密鑰輪替問題 — Adobe訪問。
   * 已使用SampleAES內容的DRM元資料修復段初始化。 適用於AES128內容。
* ZD #33619 — 快速轉發一個不斷增長的播放清單內容，該播放清單內容在接近即時點時處於緩衝狀態。
   * 在特技播放模式下穿越即時點時處理案例。
* ZD #34151 - TimedMetadata對象順序不正確。
   * 如果兩個TimedMetadata事件屬於時間軸中的同一時間，則它們按隨機順序出現。 在清單中保持其原始順序。
* ZD #34189 — 嘗試開始廣告中斷時出現問題。
   * 問題是SSAI廣告使用不連續性縫製。 原因是當我們尋找這些廣告的開始時，我們搜索一個關鍵幀，但是我們找不到它。 原因是廣告的最小音頻時間戳早於最小視頻時間戳。 因此，我們最終在錯誤的fragmentDump資料中搜索關鍵幀。 已修復。
* ZD #34528 — 在FireTV第三代轉換器上，視頻解析度不會超過640x360。
   * 已增強修復功能，以包括最新韌體更新。
* ZD #34793 - TVSDK 2.5.x用於在VideoEngine假定auditySettings可用而它們不可用時與自定義內容解析程式崩潰。
   * 由於對空共用指針(auditudeSettings)的函式調用，故障發生。 在VideoEngineTimeline::placeToSourceTimeline()中添加了條件檢查，以確保在調用該對象的任何內容之前auditudeSettings可用。
* ZD #32584 — 無法訪問中顯示的完整資訊 &lt;extensions> VAST響應的節點。
   * 解決了XML分析的問題，現在NetworkAdInfo提供了在 &lt;extensions> 的下界。
* ZD #35086 — 如果存在特定的VMAP響應，則無法從播放器獲取完整的擴展資料。
   * 此問題特定於擴展xml，因為如果擴展xml在屬性值中有雙引號，則XML分析無效。 已解決問題。

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 — 播放會話，啟用Webview遠程調試。
   * 預設情況下，WebViewDebbuging設定為False。 要啟用調試，請使用setWebContentsDebuggingEnabled(true)通過應用程式設定為true。
* ZenDesk#33011 — 如果存在失敗的CRS請求，則無法解決廣告時間線。
   * 當CRS對廣告的請求失敗時，時間線被解決，剩餘的廣告被播放。
* ZenDesk#34528 — 在FireTV第三代轉換器上，視頻解析度不會升級到640x360以上。
   * 視頻解析度以比特率切換方式切換。
* ZenDesk#33192 — 當通過AudioUpdatedEventListener::onAudioUpdated檢索軌道時，AudioTrack的名稱為空。
   * 在FireTV Stick上的幾種情況下，當沒有實際音頻更新時，onAudioUpdate事件將被激發。 這個現在修好了。

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata自定義標籤訂閱無效。
   * 我們將ID3資料作為位元組陣列（以支援APIC或泛型資料）返回給客戶端，而在1.4返回字串中。 位元組陣列不處理以空值結尾的字元本身，因此它向客戶端顯示特殊字元。 此問題現已解決。
* Zendesk#32670 — 播放器未故障切換到冗餘播放清單
   * 此操作現在正常，且setNetworkDownVerificationUrl正如預期工作。
* Zendesk#32369 — 隱藏標題顯示不同顏色的垃圾或工件。
   * CC故障問題已在最新版本中解決
* Zendesk#25590 — 增強：TVSDKcookie儲存（C++到Java™）
   * Android™ TVSDK現在支援在Java™層（儲存在Android™應用程式的CookieStore中）和C++ TVSDK層之間訪問Cookie。
* Zendesk#32252 - TVSDK_Android_2.5.2.12似乎沒有PTPLAY-20269的修復。此問題已修復並整合到2.5.2分支。
* Zendesk#31806 - PREPARING Player中的Auditude棒處於「正在準備」狀態，因為響應xml有空標籤。 問題已解決。
* Zendesk#31727 - TVSDK 2.5隱藏標題字元被刪除或拼錯。
   * 問題已解決，我們不會刪除/錯誤拼寫任何字元。
* Zendesk#31485 - DrmManager,2.5版
   * 通過新的DrmManager（上下文）建立DrmManager時出現一些問題。 已實現DRMService類，該類將提供DRMManager。
* Zendesk#32794- 1080P解析度流在Android™上不播放。
   * 我們已更改SizeAvailableEvent。 以前， `getHeight()` 和 `getWidth()` 2.5中的SizeAvailableEvent方法，用於返回由媒體格式返回的幀高和幀寬。 它現在分別返回由解碼器返回的輸出高度和輸出寬度。
* Zendesk #19359Flash Player崩潰，原因是#EXT-X-FAXS-CM屬性在設定級清單中的位置。
   * #EXT-X-FAXS-CM標籤必須始終出現在頂部播放清單中，然後才能在播放清單中顯示單個比特率或段。

**Android™ TVSDK 2.5.2**

* Zendesk#17305非不透明背景的隱藏字幕中的偽像。
將公開TextFormat中的setTreatSpaceAsAlphaNum屬性。 預設情況下，屬性為False。 在客戶端中將屬性設定為True以解決暗空間問題。

* Zendesk#25097 CC顯示器具有具有CC設定的視覺對象。
將公開TextFormat中的setTreatSpaceAsAlphaNum屬性。 預設情況下，屬性為False。 在客戶端中將屬性設定為True以解決暗空間問題。

* TVSDK播放器#31620用戶代理字串被截斷。
用戶代理字串將在128個字元後不再被截斷。
Adobe Primetime版本字串已添加到系統用戶代理。

* Zendesk #30809 Missing SEEK_END事件阻止應用轉換到播放狀態。
* Zendesk #30415 Closed Caption的「青色」顏色現在與黃金時段TVSDK的先前版本相比呈藍色（綠松石色）的較深色。

   顏色從「深青色」更改為「青色」。

* Zendesk #30727 VOD廣告未下載/解析。

   在VMAP XML中，如果有空的VAST標籤，而沒有顯式結束標籤(「&lt;/vast>&#39;)後面沒有換行符，則VMAP XML無法正確解析，廣告可能無法播放。

**Android™ TVSDK 2.5.1**

* 特定於設備（三星Galaxy頁籤4）崩潰；VOD DRM LBA，帶Auditude，點擊廣告。
* VHL — 從偏移量開始內容時發送的心跳呼叫不正確。
* 播放VPAID廣告時，VHL心跳呼叫事件:type:播放廣告丟失。
* 進入「完成」狀態後，播放器將返回SKIP adBreakPolicy的PLAYING狀態，用於後滾廣告。
* Cookie未附加到傳出廣告回調。
* 廣告提示點不可見。
* 不載入帶有獨立EAC3 SAP跟蹤的HLS。
* 播放器在恢復媒體播放器後，TVSDK接收螢幕開啟意圖時崩潰。

## 已知問題和限制 {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7支援最多五個廣告的並行解析。
* 在VMAP響應的情況下，單個Ad中斷中的Ad調用同時進行，並且Ad中斷被順序地解析。
* 在FER的情況下，每個機會中的Ad呼叫被並行解決。

### 以前版本中的已知問題和限制{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* 不支援同時多個VMAP廣告中斷。

**Android™ TVSDK 2.5.3**

此版本有以下問題：

* 即時視頻播放在低端設備上可能存在音頻 — 視頻同步問題，或者網路狀況不佳。
* 對於FER流，virtualTime和localTime可能不同。 而且，帶偏移的FER不起作用。
* 查找「Late Binding Audio（延遲綁定音頻）」內容時，回放可能會卡住。
* 對於LIVE內容，間歇性的webVTT字幕可能會變得不同步。
* 在廣告斷點後，可以間歇地快速回放幾幀。
* 有時，即使播放廣告，三重包裝廣告分段也會引發303個錯誤。

**Android™ TVSDK 2.5.2**

此版本有以下問題：

* 即時視頻播放在低端設備上可能存在音視頻同步問題。
* 當尋找到VOD媒體的末端時，回放可能會停止。
* 對於FER流，virtualTime和localTime可能不同。 另外，帶偏移的FER不起作用。

**Android™ TVSDK 2.5.1**

此版本的TVSDK存在以下問題：

* 即時視頻播放在低端設備上可能存在音視頻同步問題。
* 對於FER流，virtualTime和localTime可能不同。 另外，帶偏移的FER不起作用。
* 在VMAP XML中，如果有空的VAST標籤，而沒有顯式結束標籤(&lt;/vast>)，如果後面沒有換行符，則VMAP XML無法正確解析，廣告可能無法播放。
* 不支援VPAID後滾。

## 有用的資源 {#helpful-resources}

* [系統要求](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-requirements.html?lang=en)
* [《 TVSDK 2.7 for Android™程式設計師指南》](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2.7-overview-prod-audience-guide.html?lang=en)
* [TVSDK Android™ Javadoc for API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android™ C++ API文檔](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html)  — 每個Java™類都有相應的C++類，而C++文檔包含的解釋性資料比Java™文檔更多，因此請參閱C++文檔以更深入地瞭解Java™ API。
* [《 TVSDK 1.4到2.5 for Android™(Java™)遷移指南》](https://experienceleague.adobe.com/docs/primetime/migration/tvsdk-14-25-android.html?lang=en)
* 有關處理螢幕開/關方案，請參閱 `Application_Changes_for_Screen_On_Off.pdf` 檔案。
* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://experienceleague.adobe.com/docs/primetime.html) 的子菜單。
