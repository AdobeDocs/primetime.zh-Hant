---
title: Android適用的TVSDK 2.4.1發行說明
description: Android適用的TVSDK 2.4.1發行說明說明，說明TVSDK Android 2.4.1中的新功能和支援功能，以及已知問題和限制。
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Android適用的TVSDK 2.4.1發行說明 {#tvsdk-for-android-release-notes}

Android適用的TVSDK 2.4.1發行說明說明，說明TVSDK Android 2.4.1中的新功能和支援功能，以及已知問題和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe即將發行適用於Android的TVSDK 2.4.1。

若要使用此版本的TVSDK，請確保您的系統符合上所述的要求。 [系統需求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

您可以在這裡找到檔案：

·線上說明系統TVSDK 2.4 for Android說明

· [適用於Android Java API的Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs是最終權威，因為它們是直接從TVSDK原始程式碼自動產生的。

· [Android C++ API適用的C++ API檔案TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每個Java類別都有對應的C++類別，且C++檔案包含的說明資料比Javadocs更多，因此請參閱C++檔案以深入瞭解Java API。

·移轉指南([Android適用的TVSDK 2.4移轉指南](../migration-guides/tvsdk-14-25-android.md))

本指南說明您將根據TVSDK 1.4的應用程式移轉至根據TVSDK 2.4的應用程式時需要修改的內容。

## 新功能 {#new-features}

相較於舊版，適用於Android的TVSDK 2.4.1提供許多效能改善專案。 提供高品質的觀賞體驗。

此版本包含2.4和2.4.1版的所有功能，不建議使用任何功能。

以下是2.4.1版的主要新功能：

* HLS 4版功能

   * **視訊播放** （播放、暫停、搜尋）搭配播放器控制，適用於即時、線性和VOD資料流。
   * **隱藏式字幕。** TVSDK可以顯示608/708隱藏式字幕，其中包含字型、字型大小、顏色和背景選擇。 它也可以支援有統計字幕的視訊，並在語言曲目之間切換（如果有的話）。
   * **特技播放模式** 支援使用I-Frame的HLS資料流快速前進和倒帶。 內容上的所有視訊播放控制項都可運作。 低速動作（前進）適用於速率介於0到1之間的外部視訊播放模式。
   * **最適化位元速率(ABR)** 可讓播放器根據網路和其他條件，動態選取要播放的相同內容資料流的多個版本。 您可以動態設定引數，或在資訊清單檔案中設定引數，以在積極、溫和和保守的選取原則中選取。
   * **位元組範圍** 啟用單一TS檔案以包含多個TS區段。
   * **替代音訊轉譯** 讓播放器能在可用音軌之間切換。
   * **ID3支援。** TVSDK可以播放包含ID3音訊中繼資料的HLS音訊和視訊串流，例如藝人姓名、職稱和專輯。
   * **容錯移轉。 儘管主機伺服器、播放清單檔案和區段失敗，**TVSDK仍會使用策略來繼續不中斷的播放。
   * **多聲道音訊傳遞(DD+)。** TVSDK可將Dolby Digital Plus音訊(E-AC3)資料傳送至支援的硬體。

* 內容保護功能

   * **HLS的DRM。** 所有視訊播放API都可搭配受Adobe存取保護的加密視訊內容運作。 支援下列DRM功能：

      * 授權輪換
      * 金鑰輪換
      * 授權快取
      * 原則時間
      * IV旋轉

* **AES 128播放。** TVSDK可以播放金鑰大小為128位元的進階加密標準(AES) HLS內容。
* **受保護的HLS (PHL)** 提供有限的一組預先建立的DRM原則(Adobe存取提供的子集)，以啟用即時和VOD資料流的輕量型DRM over HLS。

* 廣告/替代內容和營利功能

   * **追蹤伺服器端插入的廣告。** TVSDK可追蹤Adobe雲端廣告插入服務所插入的廣告。 它支援VAST2、VAST3和VMAP格式的線性廣告，適用於VOD和即時/線性資料流。
   * **自訂HLS標籤。** TVSDK使用其 `MediaPlayerConfig` 類別，以在自訂HLS標籤出現在資料流中時通知播放器應用程式。
   * **使用者端廣告插入。** Auditude廣告插入程式庫可與Adobe Auditude伺服器搭配使用，在前段、中段或後段位置，將動態插入的廣告解析為即時、線性和VOD內容。
   * **自訂廣告解析程式。** 此 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 介面可讓您實作自訂廣告/替代內容解析程式，並註冊自訂機會偵測器以搭配TVSDK使用。 此 `TestAdResolver` 和 `AuditudeResolver` 類別提供實作內容解析器的C++範例。 如需Javascript範例，請前往 `samples/jspsdk/testapp/psdk.js`.
   * **一致的廣告行為。** 使用 `AdPolicySelector` 介面，可在內容中出現廣告時，針對搜尋和特技播放等操作，啟用所有播放器的一致行為。 如果您未實作自己的工具，TVSDK會使用 `DefaultAdPolicySelector`.
   * **移除/取代C3廣告。** 使用適當的TVSDK API移除自訂內容範圍，並動態插入新廣告，無需額外的準備工作。 直播/線性內容播出後，立即可供點播使用（無需清理）時，此方法會很實用。

以下是2.4版的主要新功能：

* **立即開啟以進行VOD和即時** 當您啟用立即開啟時，TVSDK會在播放開始之前初始化並緩衝媒體。 因為您可以啟動多個 `MediaPlayerItemLoader` 您可以在背景同時緩衝多個串流。 當使用者變更頻道，並且串流已正確緩衝時，新頻道上的播放立即開始。 TVSDK 2.4也支援即時上線的即時資料流。 即時視窗移動時會重新緩衝即時資料流。

* **效能改良**新的TVSDK 2.4架構提供各種效能改良：

   * **子細分** - TVSDK進一步縮小每個片段的大小，以儘快開始播放。
   * **平行廣告下載** - TVSDK會在點選廣告插播之前預先擷取與內容播放並行的廣告，因此可順暢地播放廣告和內容。
   * **延遲廣告解析度**  — 有了此功能，我們就不會等到非前段廣告解決後再開始播放，因此縮短了啟動時間。 除非解決所有廣告，否則仍不允許搜尋和特技播放等API。

* **MP4內容播放**

此版本的TVSDK支援MP4播放為主要內容。

* **持續性網路連線**

TVSDK會維護一組可重複使用的網路連線，因此不會產生為每個網路要求建立和摧毀網路連線的額外負荷。

* **以解析度為基礎的輸出保護**

此功能將播放限制繫結至特定解析度，提供更精細的DRM控制項。

* **以最適化位元速率(ABR)進行特技播放**

此功能可讓TVSDK在特技播放模式中切換iFrame串流。 您可以使用非iFrame設定檔，以較低速度進行特技播放。

* **更流暢的特技遊戲**

這些改善專案可增強使用者體驗：

·在特技播放期間，根據頻寬和緩衝區設定檔選擇最適化位元速率和影格速率

·使用主資料流而非IDR資料流，以取得最高30 fps的快速播放。

* **改善ABR邏輯**

新的ABR邏輯是以緩衝區長度、緩衝區長度變更速率，以及測量的頻寬為基礎。 這可確保ABR在頻寬波動時選擇正確的位元速率，並透過監控緩衝區長度變更的速率，最佳化位元速率切換的實際發生次數。

* **帳單**

TVSDK會根據客戶銷售合約自動收集量度，以產生開立帳單所需的定期使用報表。 在每個資料流開始事件上，TVSDK會使用Adobe Analytics資料插入API將計費量度（例如內容型別、廣告插入啟用旗標，以及drm啟用旗標）根據計費資料流的持續時間傳送至Adobe Analytics Primetime擁有的報表套裝。 這不會干擾或納入客戶自己的Adobe Analytics報表套裝或伺服器呼叫。 系統會根據要求定期傳送此計費使用報告給客戶。 這是計費功能的第一個階段，僅支援使用計費。 您可以使用本檔案中說明的API，根據銷售合約進行設定。

## 支援的功能 {#supported-features}

適用於Android 2.4的TVSDK支援許多您可實作的功能，以將功能新增至視訊應用程式。

>[!NOTE]
>
>在下方的功能矩陣表中，√表示目前版本支援該功能。

### 核心播放功能 {#core-playback-features}

| **功能** | **內容型別** | **HLS** | **虛線** |
|---|---|---|---|
| 一般播放（播放、暫停、搜尋） | VOD +即時 | √ | √ （僅限VOD） |
| FER — 一般播放（播放、暫停、搜尋） | FER VOD | √ | 不支援 |
| MP3 | VOD | 不支援 | 不支援 |
| MP4內容播放 | VOD | √ | √ |
| 最適化位元速率切換邏輯 | VOD +即時 | √ | 不支援 |
| 僅限音訊的播放 | VOD +即時 | √ | 不支援 |
| 隱藏式字幕 — 608/708 | VOD +即時 | √ | √ （僅限VOD） |
| 隱藏式字幕 — WebVTT | VOD +即時 | √ | √ （僅限VOD） |
| 資訊清單容錯移轉 | VOD +即時 | √ | √ （僅限VOD） |
| 進階容錯移轉 | VOD +即時 | √ | √ （僅限VOD） |
| QoS和播放器通知 | VOD +即時 | √ | √ （僅限VOD） |
| 支援Cookie標頭 | VOD +即時 | √ | √ （僅限VOD） |
| 支援自訂標頭 | VOD +即時 | 不支援 | 不支援 |
| 設定緩衝區控制引數 | VOD +即時 | √ | √ （僅限VOD） |
| 設定最適化位元速率控制 | VOD +即時 | √ | √ （僅限VOD） |
| 自訂資訊清單標籤(HLS) /事件資料流（破折號） | VOD +即時 | √ | √ （僅限VOD） |
| 延遲傳送的音訊 | VOD +即時 | √ | √ （僅限VOD） |
| 302重新導向 | VOD +即時 | √ | √ （僅限VOD） |

### 進階播放功能 {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容型別</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虛線</strong></td> 
  </tr>
  <tr>
   <td>有位移的播放</td> 
   <td>即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>僅限音訊的播放</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>特技播放 </td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>Smooth Trick Play （含ABR）</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>ID3剖析(HLS) /計時中繼資料(DASH)</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>中斷 </td> 
   <td>VOD +即時</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>立即開啟</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不連續標籤支援(HLS) </li> 
     <li>多句點（破折號）</li> 
    </ul> </td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>302重新導向粘性</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>√ （僅限VOD）</td> 
  </tr>
  <tr>
   <td>縮圖清除(Iframe和JPEG)</td> 
   <td>VOD +即時</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>串流完整性 </td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
 </tbody>
</table>

### 核心Ad Insertion功能(CSAI) {#core-ad-insertion-features-csai}

| **功能** | **內容型別** | **HLS** | **虛線** |
|---|---|---|---|
| 一般播放，啟用廣告 | VOD +即時 | √ | √ （僅限VOD前段） |
| 已啟用廣告的FER內容 | VOD | √ | 不支援 |
| 預設廣告行為 | VOD +即時 | √ | √ （僅限VOD前段） |
| VAST 2.0/3.0 | VOD +即時 | √ | √ （僅限VOD前段） |
| VMAP 1.0 | VOD +即時 | √ | √ （僅限VOD前段） |
| MP4廣告 | VOD +即時 | √ （來自CRS） | √ （來自CRS，僅限前段） |

### 進階Ad Insertion功能(CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容型別</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虛線</strong></td> 
  </tr>
  <tr>
   <td>啟用廣告的Trick Play</td> 
   <td>VOD +即時</td> 
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
   <td>目標定位引數</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>√ （僅限VOD前段）</td> 
  </tr>
  <tr>
   <td>自訂引數</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>√ （僅限VOD前段）</td> 
  </tr>
  <tr>
   <td>自訂廣告行為</td> 
   <td>VOD +即時</td> 
   <td>√</td> 
   <td>√ （僅限VOD前段）</td> 
  </tr>
  <tr>
   <td>自訂廣告標籤</td> 
   <td>即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>自訂廣告解析程式</td> 
   <td>VOD +即時</td> 
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
   <td>C3廣告取代 </td> 
   <td>VOD +即時</td> 
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
     <li>不連續標籤支援 — SSAI (HLS) </li> 
     <li>多句點（破折號）</li> 
    </ul> </td> 
   <td>VOD +即時</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>隨附廣告、橫幅廣告和可點按廣告</td> 
   <td>VOD +即時</td> 
   <td>√ </td> 
   <td>√ （僅限VOD前段）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD +即時</td> 
   <td>√ (JS) </td> 
   <td>√ （僅限VOD前段）</td> 
  </tr>
  <tr>
   <td>早期廣告結束</td> 
   <td>即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>規則型Creative VOD +即時優先順序</td> 
   <td>VOD +即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>CRS規則 </td> 
   <td>VOD +即時</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
 </tbody>
</table>

## 內容保護功能 {#content-protection-features}

| **功能** | **內容型別** | **HLS** | **虛線** |
|---|---|---|---|
| AES加密 | VOD +即時 | √ | √ （僅限VOD） |
| AES加密範例 | VOD +即時 | √ |  |
| 代碼化的資料流 | VOD +即時 | √ |  |
| DRM | VOD +即時 | 僅限Primetime DRM （未來：Widevine） | 僅限Widevine |
| 外部播放(RBOP) | VOD +即時 | 僅限Primetime DRM | 不支援 |
| 授權輪換 | VOD +即時 | 僅限Primetime DRM | 不支援 |
| 金鑰輪換 | VOD +即時 | 僅限Primetime DRM | 不支援 |

### 整合功能 {#integration-features}

| **功能** | **內容型別** | **HLS** | **虛線** |
|---|---|---|---|
| Adobe Analytics VHL整合 | VOD +即時 | √ | √ |
| 帳單 | VOD +即時 | √ | 不支援 |

## 不支援的功能 {#features-not-supported}

此版本的TVSDK不支援：

* 廣告中斷。
* 特技遊戲中的慢動作。
* 使用MP4內容進行搜尋和點播。
* 包含MP4主要內容的廣告插入。
* 在廣告播放時搜尋。
* 使用純音訊媒體播放廣告。

## 已知問題和限制 {#known-issues-and-limitations}

此版本的TVSDK有下列問題：

* 裝置特定(Samsung Galaxy Tab 4)當機VOD DRM LBA，具有稽核並點選廣告
* 不會針對特定內容播放後段廣告。
* 將隱藏式字幕設定為CJK語言無法運作。
* 視訊可以從VOD和即時之間的特技模式自動結束。
* VHL — 從位移開始內容時，會傳送錯誤的心率呼叫。
* 播放VPAID廣告時，事件的VHL心率呼叫:type:播放廣告遺失。
* 即使已選取adBreakPolicy SKIP，也會播放前段廣告。
* 進入完成狀態後，播放器會針對後置廣告返回具有SKIP adBreakPolicy的播放狀態。

如果沒有視訊，就沒有檢視區尺寸，如果沒有檢視區尺寸，您將無法顯示註解的任何圖形。

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://experienceleague.adobe.com/docs/primetime.html) 頁面。
