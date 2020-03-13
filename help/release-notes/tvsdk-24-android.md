---
title: Android專用TVSDK 2.4.1版本注意事項
seo-title: Android專用TVSDK 2.4.1版本注意事項
description: TVSDK 2.4.1 for Android發行說明說明TVSDK Android 2.4.1中新增和支援的功能以及已知問題和限制。
seo-description: TVSDK 2.4.1 for Android發行說明說明TVSDK Android 2.4.1中新增和支援的功能以及已知問題和限制。
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Android專用TVSDK 2.4.1版本注意事項 {#tvsdk-for-android-release-notes}

TVSDK 2.4.1 for Android發行說明說明TVSDK Android 2.4.1中新增和支援的功能以及已知問題和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe正在推出Android專用的TVSDK 2.4.1。

若要使用此版本的TVSDK，請確定您的系統符合「系統需求」中所述 [的需求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)。

您可從以下位置找到檔案：

·適用於Android說明的線上說明系統TVSDK 2.4

· [Android Java API專用的Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadoc是終極授權，因為它們會直接從TVSDK原始碼自動產生。

· [C++ API檔案TVSDK 2.4 for Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每個Java類都有相應的C++類，而C++文檔包含的解釋性內容比Javadoc更多，因此，請查閱C++文檔以更深入地瞭解Java API。

·移轉指南([TVSDK 2.4 for Android移轉指南](../migration-guides/tvsdk-14-25-android.md))

本指南說明您需要修改哪些項目，才能將以TVSDK 1.4為基礎的應用程式移轉至以TVSDK 2.4為基礎的應用程式。

## 新功能 {#new-features}

適用於Android的TVSDK 2.4.1提供比舊版更多的效能改進。 提供高品質的檢視體驗。

此版本包含2.4和2.4.1版的所有功能，不再提倡任何功能。

2.4.1版的主要新功能如下：

* HLS第4版功能

   * **視訊播放** （播放、暫停、搜尋）及即時、線性和VOD串流的播放器控制。
   * **隱藏字幕。** TVSDK可顯示608/708隱藏字幕，其中包含多種字型、字型大小、顏色和背景。 此外，它還可支援具有捲動標題的視訊，並在語言軌道之間切換（如果有的話）。
   * **特技播放模式** ，可支援使用I-Frames的HLS串流的快進和倒轉。 所有視訊播放控制項都可在內容上運作。 慢動作（前向）適用於速率介於0和1之間的外部視訊播放模式。
   * **可調式位元速率(ABR)** ，可讓播放器根據網路和其他條件，動態選取要播放相同內容串流的多個版本。 您可以動態設定參數或在資訊清單檔案中設定參數，以選擇激進、中和和保守的選擇原則。
   * **位元組範圍** ，使單個TS檔案能夠包含多個TS段。
   * **替代的音訊轉譯** ，讓播放器可在可用的音軌之間切換。
   * **ID3支援。** TVSDK可播放包含ID3音訊中繼資料（例如藝術家姓名、標題和相簿）的HLS音訊和視訊串流。
   * **故障切換。 **TVSDK使用策略來繼續不間斷播放，儘管主機伺服器、播放清單檔案和區段失敗。
   * **多聲道音訊傳遞(DD+)。** TVSDK可將Dolby Digital Plus音訊(E-AC3)資料傳遞至支援硬體。

* 內容保護功能

   * **HLS的DRM** 所有視訊播放API都可搭配Adobe Access保護的加密視訊內容運作。 支援下列DRM功能：

      * 授權輪換
      * 鍵旋轉
      * 授權快取
      * 策略時間
      * IV旋轉

* **AES 128播放。** TVSDK可播放128位元的進階加密標準(AES)HLS內容。
* **受保護的HLS(PHLS)** ，提供有限的預建DRM原則集（Adobe Access提供的子集），讓即時和VOD串流的HLS上的DRM更輕量。

* 廣告／替代內容與獲利功能

   * **追蹤伺服器端插入廣告。** TVSDK可追蹤Adobe Cloud廣告插入服務所插入的廣告。 它支援VOD和即時／線性串流的VAST2、VAST3和VMAP格式的線性廣告。
   * **自訂HLS標籤。** 當自訂HLS標籤出 `MediaPlayerConfig` 現在串流中時，TVSDK會使用其類別來啟用通知播放器應用程式。
   * **用戶端廣告插入。** Auditude廣告插入程式庫可與Adobe Auditude伺服器搭配使用，以解析廣告，以便在前段、中段或後段位置動態插入即時、線性和VOD內容。
   * **自訂廣告解析器。** 此 `ContentResolver, OpportunityGenerator,` 和介 `MediaPlayerClientFactory` 面可讓您建置自訂廣告／替代內容解析程式，並註冊自訂商機偵測器以搭配TVSDK運作。 這些 `TestAdResolver` 和 `AuditudeResolver` 類提供了實現內容解析器的C++示例。 您可在找到Javascript範例 `samples/jspsdk/testapp/psdk.js`。
   * **一致的廣告行為。** 使用介 `AdPolicySelector` 面可讓所有播放器的行為一致，例如在內容中顯示廣告時進行尋找和特技播放。 如果您未實作自己的，TVSDK會使用 `DefaultAdPolicySelector`。
   * **移除／取代C3廣告。** 使用適當的TVSDK API來移除自訂內容範圍，並動態插入新廣告，毋需額外的準備工作。 當廣播即時／線性內容後，即時隨選提供而不需進行清理時，此功能就十分方便。

以下是2.4版的主要新功能：

* **VOD和即時的立即啟動** ：當您啟用即時啟動時，TVSDK會在播放開始前初始化媒體並緩衝媒體。 由於您可以在背景同 `MediaPlayerItemLoader` 時啟動多個例項，因此可以緩衝多個串流。 當使用者變更頻道，而串流已正確緩衝時，新頻道上的播放會立即開始。 TVSDK 2.4也支援即時串流的Instant On。 即時視窗移動時，即時串流會重新緩衝。

* **效能改進**全新的TVSDK 2.4架構提供多種效能改進：

   * **子分段** - TVSDK進一步縮減每個片段的大小，以盡快開始播放。
   * **平行廣告下載** - TVSDK會在點擊廣告插播前，平行預取與內容播放平行的廣告，因此能夠順暢地播放廣告和內容。
   * **懶惰廣告解析度** -使用此功能，我們不會等到非預先播放廣告的解析度再開始播放，因此會縮短啟動時間。 在所有廣告都解決之前，仍不允許搜尋和特技播放等API。

* **MP4內容播放**

此版TVSDK支援播放MP4為主要內容。

* **持續網路連線**

TVSDK會維護一組可重複使用的網路連線，因此不會產生針對每個網路要求建立和毀壞網路連線的額外負荷。

* **基於解析度的輸出保護**

此功能將播放限制與特定解析度相關聯，提供更精細的DRM控制。

* **具自適應位元速率(ABR)的特技播放**

此功能可讓TVSDK在iFrame串流之間切換，同時處於特技播放模式。 您可以使用非iFrame描述檔，以較低的速度進行特技播放。

* **更順暢的特技播放**

這些改良功能可增強使用者體驗：

·根據頻寬和緩衝區設定檔，在特技播放期間自適應位元速率和影格速率選擇

·使用主串流（而非IDR串流），以快速播放高達30 fps。

* **改良的ABR邏輯**

新的ABR邏輯基於緩衝長度、緩衝長度變化速率和測量頻寬。 這確保了ABR在頻寬波動時選擇正確的比特率，並且還通過監視緩衝器長度變化的速率來優化比特率切換的實際發生的次數。

* **帳單**

TVSDK會自動收集量度，並遵守客戶銷售合約，以產生計費所需的定期使用報告。 在每個串流開始事件上，TVSDK都會使用Adobe Analytics資料插入API，將計費量度(例如內容類型、啟用廣告插入的標幟，以及啟用drm的標幟（根據計費串流的持續時間）傳送至Adobe Analytics Primetime擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 此帳單使用報表會按要求定期傳送給客戶。 這是計費功能的第一階段，僅支援使用計費。 您可使用說明檔案中所述的API，根據銷售合約來設定此API。

## 支援的功能 {#supported-features}

適用於Android 2.4的TVSDK支援許多您可實作的功能，以新增功能至視訊應用程式。

>[!NOTE]
>
>在下方的功能矩陣表格中，√表示目前版本支援此功能。

### 核心播放功能 {#core-playback-features}

| **功能** | **內容類型** | **HLS** | **虛線** |
|---|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD + Live | √ | √（僅限VOD） |
| FER —— 一般播放（播放、暫停、搜尋） | FER VOD | √ | 不支援 |
| MP3 | VOD | 不支援 | 不支援 |
| MP4內容播放 | VOD | √ | √ |
| 自適應位速率切換邏輯 | VOD + Live | √ | 不支援 |
| 僅限音訊播放 | VOD + Live | √ | 不支援 |
| 隱藏字幕- 608/708 | VOD + Live | √ | √（僅限VOD） |
| 隱藏字幕- WebVTT | VOD + Live | √ | √（僅限VOD） |
| 資訊清單容錯移轉 | VOD + Live | √ | √（僅限VOD） |
| 高級故障切換 | VOD + Live | √ | √（僅限VOD） |
| QoS和播放器通知 | VOD + Live | √ | √（僅限VOD） |
| 支援Cookie標題 | VOD + Live | √ | √（僅限VOD） |
| 支援自訂標題 | VOD + Live | 不支援 | 不支援 |
| 設定緩衝器控制參數 | VOD + Live | √ | √（僅限VOD） |
| 設定自適應位元速率控制 | VOD + Live | √ | √（僅限VOD） |
| 自訂資訊清單標籤(HLS)/事件串流(DASH) | VOD + Live | √ | √（僅限VOD） |
| 延遲裝訂音訊 | VOD + Live | √ | √（僅限VOD） |
| 302重新導向 | VOD + Live | √ | √（僅限VOD） |

### 進階播放功能 {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容類型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虛線</strong></td> 
  </tr>
  <tr>
   <td>具有偏移的播放</td> 
   <td>即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>僅限音訊播放</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>流暢的特技播放（使用ABR）</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>ID3剖析(HLS)/計時中繼資料(DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>封鎖期 </td> 
   <td>VOD + Live</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>立即啟動</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不連續標籤支援(HLS) </li> 
     <li>多句點(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>302重新導向嚴格性</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD）</td> 
  </tr>
  <tr>
   <td>縮圖拖曳（Iframe和JPEG）</td> 
   <td>VOD + Live</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>串流完整性 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
 </tbody>
</table>

### 核心廣告插入功能(CSAI) {#core-ad-insertion-features-csai}

| **功能** | **內容類型** | **HLS** | **虛線** |
|---|---|---|---|
| 一般播放，啟用廣告 | VOD + Live | √ | √（僅限VOD預卷） |
| 啟用廣告的FER內容 | VOD | √ | 不支援 |
| 預設廣告行為 | VOD + Live | √ | √（僅限VOD預卷） |
| VAST 2.0/3.0 | VOD + Live | √ | √（僅限VOD預卷） |
| VMAP 1.0 | VOD + Live | √ | √（僅限VOD預卷） |
| MP4廣告 | VOD + Live | √（來自CRS） | √（來自CRS，僅預先登記） |

### 進階廣告插入功能(CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容類型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虛線</strong></td> 
  </tr>
  <tr>
   <td>啟用廣告的特技播放</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>僅限廣告 </td> 
   <td>VOD</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>定位參數</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自訂參數</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自訂廣告行為</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自訂廣告標籤</td> 
   <td>即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>自訂廣告解析器</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>Freewheel自訂廣告解析程式</td> 
   <td>VOD</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>C3廣告替換 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>延遲廣告載入</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不連續標籤支援- SSAI(HLS) </li> 
     <li>多句點(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>配套廣告、橫幅廣告和可點選廣告</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√(JS) </td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>提早退出廣告</td> 
   <td>即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>以規則為基礎的創意VOD +即時優先順序</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>CRS規則 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
 </tbody>
</table>

## 內容保護功能 {#content-protection-features}

| **功能** | **內容類型** | **HLS** | **虛線** |
|---|---|---|---|
| AES加密 | VOD + Live | √ | √（僅限VOD） |
| 範例AES加密 | VOD + Live | √ |  |
| Token化串流 | VOD + Live | √ |  |
| DRM | VOD + Live | 僅限Primetime DRM(未來：Widevine) | 僅限Widevine |
| 外部播放(RBOP) | VOD + Live | 僅限Primetime DRM | 不支援 |
| 授權輪換 | VOD + Live | 僅限Primetime DRM | 不支援 |
| 鍵旋轉 | VOD + Live | 僅限Primetime DRM | 不支援 |

### 整合功能 {#integration-features}

| **功能** | **內容類型** | **HLS** | **虛線** |
|---|---|---|---|
| Adobe Analytics VHL整合 | VOD + Live | √ | √ |
| 帳單 | VOD + Live | √ | 不支援 |

## 不支援的功能 {#features-not-supported}

此TVSDK版本不支援：

* 封鎖廣告。
* 玩魔術的慢動作。
* 尋找並試用MP4內容。
* 以MP4主要內容插入廣告。
* 在廣告播放時尋找。
* 使用純音訊媒體播放廣告。

## 已知問題和限制 {#known-issues-and-limitations}

此TVSDK版本有下列問題：

* 裝置特定(Samsung Galaxy Tab 4)使用auditude和點按廣告讓VOD DRM LBA當機
* 特定內容不會播放後置廣告。
* 將關閉標題設定為CJK語言無效。
* 視訊可自動在VOD和即時之間跳出特技模式。
* VHL —— 當我們從偏移開始內容時，會傳送錯誤的心率呼叫。
* 播放VPAID廣告時，VHL心率earte呼叫event:type:play廣告遺失。
* 即使選擇adBreakPolicy SKIP，前段廣告仍會播放。
* 進入「完整」狀態播放器後，使用SKIP adBreakPolicy返回「播放」狀態，以播放後轉播廣告。

沒有視訊，就沒有視訊區尺寸，沒有視訊區尺寸，就無法顯示標題的任何圖形。

## 有用的資源 {#helpful-resources}

* 請參閱 [Adobe Primetime學習與支援頁面的完整說明檔案](https://helpx.adobe.com/support/primetime.html) 。