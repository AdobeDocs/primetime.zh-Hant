---
title: 《 TVSDK 2.4.1 for Android發行說明》
description: TVSDK 2.4.1 for Android發行說明描述了TVSDK Android中新增和支援的功能以及已知問題和限制2.4.1。
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# 《 TVSDK 2.4.1 for Android發行說明》 {#tvsdk-for-android-release-notes}

TVSDK 2.4.1 for Android發行說明描述了TVSDK Android中新增和支援的功能以及已知問題和限制2.4.1。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe正在發佈適用於Android的TVSDK 2.4.1。

要使用此版本的TVSDK，請確保您的系統滿足上所述的要求 [系統要求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)。

您可以在此處找到文檔：

·用於Android幫助的聯機幫助系統TVSDK 2.4

· [用於Android Java API的Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadoc是終極權威，因為它們是直接從TVSDK原始碼自動生成的。

· [C++ API文檔TVSDK 2.4（適用於Android C++ API）](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每個Java類都有相應的C++類，而C++文檔包含的解釋性材料比Javadoc更多，因此請參閱C++文檔，以便更深入地瞭解Java API。

·遷移指南([《 TVSDK 2.4 for Android遷移指南》](../migration-guides/tvsdk-14-25-android.md))

本指南說明了將基於TVSDK 1.4的應用程式遷移到基於TVSDK 2.4的應用程式時需要修改的內容。

## 新功能 {#new-features}

用於Android的TVSDK 2.4.1與早期版本相比提供了許多效能改進。 它提供高質量的觀看體驗。

此版本包含2.4和2.4.1版的所有功能，不建議使用任何功能。

以下是2.4.1版中的關鍵新功能：

* HLS版本4功能

   * **視頻播放** （播放、暫停、搜索），播放器控制用於即時、線性和VOD流。
   * **隱藏字幕。** TVSDK可以顯示608/708隱藏字幕，其中包含字型、字型大小、顏色和背景。 它還可支援帶有捲起字幕的視頻，並在語言軌道之間切換（如果可用）。
   * **特技播放模式** 支援使用I-Frames的HLS流的快速前向和後向。 所有視頻播放控制內容的功能。 慢速運動（向前）可用於速率介於0和1之間的外部視頻回放模式。
   * **自適應比特率(ABR)** 允許播放器根據網路和其他條件動態選擇要播放的同一內容流的多個版本中的哪個版本。 可以動態設定參數或在清單檔案中設定參數，以在激進、中等和保守的選擇策略中進行選擇。
   * **位元組範圍** 啟用單個TS檔案以包含多個TS段。
   * **備用音頻格式副本** 使播放器能夠在可用的音頻軌道之間切換。
   * **ID3支援。** TVSDK可以播放包含ID3音頻元資料的HLS音頻和視頻流，如藝術家姓名、標題和相冊。
   * **故障轉移。 **儘管主機伺服器、播放清單檔案和段出現故障，TVSDK仍使用策略繼續不間斷的播放。
   * **多聲道音頻傳輸(DD+)。** TVSDK可以將杜比數字加音頻(E-AC3)資料傳遞給支援硬體。

* 內容保護功能

   * **HLS的DRM。** 所有視頻播放API都與受Adobe訪問保護的加密視頻內容配合使用。 支援以下DRM功能：

      * 許可證輪換
      * 鍵旋轉
      * 許可證快取
      * 策略時間
      * 四輪

* **AES 128回放。** TVSDK可以播放密鑰大小為128位的高級加密標準(AES)HLS內容。
* **受保護的HLS(PHLS)** 提供有限的一組預構建的DRM策略，即Adobe訪問提供的子集，以在HLS上為即時和VOD流啟用輕量級DRM。

* 廣告/備用內容和貨幣化功能

   * **伺服器端插入廣告的跟蹤。** TVSDK可以跟蹤Adobe雲廣告插入服務插入的廣告。 它支援VOD和即時/線性流的VAST2,VAST3和VMAP格式的線性廣告。
   * **自定義HLS標籤。** TVSDK使用 `MediaPlayerConfig` 類，以在流中出現自定義HLS標籤時啟用通知player應用程式。
   * **客戶端和插入。** Auditude廣告插入庫與Adobe Auditude伺服器協作，以解決廣告在預滾、中滾或後滾位置動態插入即時、線性和VOD內容。
   * **自定義廣告解析器。** 的 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 介面使您能夠實現自定義ad/替代內容解析器並註冊自定義機會檢測器以與TVSDK一起使用。 的 `TestAdResolver` 和 `AuditudeResolver` 類提供了實現內容解析器的C++示例。 您可以在以下位置找到Javascript示例： `samples/jspsdk/testapp/psdk.js`。
   * **一致的廣告行為。** 使用 `AdPolicySelector` 介面，在內容中出現廣告時，使所有玩家的行為一致，例如查找和特技播放。 如果您沒有實現自己的功能，TVSDK將使用 `DefaultAdPolicySelector`。
   * **刪除/更換C3廣告。** 使用適當的TVSDK API刪除自定義內容範圍並動態插入新廣告，而不需要額外的準備工作。 當直播/線性內容，然後立即按需提供而不進行清理時，這非常方便。

以下是2.4版的主要新功能：

* **即時播放視頻點播和直播** 啟用即時時，TVSDK會在播放開始前初始化和緩衝媒體。 因為你可以啟動多個 `MediaPlayerItemLoader` 實例同時在後台，可以緩衝多個流。 當用戶更改頻道，並且流已正確緩衝時，新頻道上的播放將立即開始。 TVSDK 2.4還支援即時流的即時開機。 當即時窗口移動時，即時流被重新緩衝。

* **效能改進**新的TVSDK 2.4體系結構帶來了各種效能改進：

   * **子分割** - TVSDK進一步縮小了每個片段的大小，以便盡快開始播放。
   * **並行廣告下載** - TVSDK在擊中廣告中斷前，先平行預取廣告，從而實現廣告和內容的無縫回放。
   * **懶惰的廣告解析度**  — 使用此功能，我們不會等待非預卷廣告的解析度再開始播放，從而縮短啟動時間。 在解決所有廣告之前，仍不允許使用搜索和特技播放等API。

* **MP4內容播放**

此版本的TVSDK支援將MP4作為主要內容進行回放。

* **永久網路連接**

TVSDK維護一組可重用的網路連接，因此它不會產生為每個網路請求建立和銷毀網路連接的開銷。

* **基於解析度的輸出保護**

此功能將回放限制與特定解析度相關聯，從而提供更精細的DRM控制項。

* **具有自適應比特率(ABR)的特技播放**

此功能允許TVSDK在iFrame流之間切換，同時處於特技播放模式。 您可以使用非iFrame配置檔案以較低的速度進行特技播放。

* **更流暢的特技播放**

這些改進增強了用戶體驗：

·在特技播放期間根據頻寬和緩衝區配置檔案進行自適應比特率和幀速率選擇

·使用主流（而不是IDR流），可快速播放高達30幀/秒。

* **改進的ABR邏輯**

新的ABR邏輯基於緩衝區長度、緩衝區長度變化率和測量的頻寬。 這確保ABR在頻寬波動時選擇正確的比特率，還通過監視緩衝器長度變化的速率來優化比特率切換的實際發生次數。

* **計費**

TVSDK自動收集度量，遵守客戶銷售合同，以生成計費所需的定期使用報告。 在每個流啟動事件上，TVSDK使用Adobe Analytics資料插入API將計費度量（如內容類型、啟用廣告插入的標誌和基於可計費流持續時間的啟用drm的標誌）發送到Adobe Analytics黃金時段擁有的報告套件。 這不會干擾或包括在客戶自己的Adobe Analytics報告套件或伺服器呼叫中。 應請求，此開單使用情況報告會定期發送給客戶。 這是僅支援使用計費的計費功能的第一階段。 可以根據銷售合同使用文檔中描述的API進行配置。

## 支援的功能 {#supported-features}

適用於Android 2.4的TVSDK支援許多功能，您可以實施這些功能來向視頻應用程式添加功能。

>[!NOTE]
>
>在下面的特徵矩陣表中，√表示當前版本支援該特徵。

### 核心播放功能 {#core-playback-features}

| **功能** | **內容類型** | **合肥光源** | **短划線** |
|---|---|---|---|
| 常規播放（播放、暫停、查找） | VOD + Live | √ | √（僅限VOD） |
| FER — 常規播放（播放、暫停、查找） | FER視頻點播 | √ | 不支援 |
| MP3 | 視頻點播 | 不支援 | 不支援 |
| MP4內容播放 | 視頻點播 | √ | √ |
| 自適應比特率切換邏輯 | VOD + Live | √ | 不支援 |
| 僅播放音頻 | VOD + Live | √ | 不支援 |
| 隱藏字幕 — 608/708 | VOD + Live | √ | √（僅限VOD） |
| 隱藏字幕 — WebVTT | VOD + Live | √ | √（僅限VOD） |
| 清單故障轉移 | VOD + Live | √ | √（僅限VOD） |
| 高級故障切換 | VOD + Live | √ | √（僅限VOD） |
| QoS和播放器通知 | VOD + Live | √ | √（僅限VOD） |
| 支援Cookie標頭 | VOD + Live | √ | √（僅限VOD） |
| 支援自定義標頭 | VOD + Live | 不支援 | 不支援 |
| 設定緩衝區控制參數 | VOD + Live | √ | √（僅限VOD） |
| 設定自適應比特率控制 | VOD + Live | √ | √（僅限VOD） |
| 自定義清單標籤(HLS)/事件流(DASH) | VOD + Live | √ | √（僅限VOD） |
| 延遲綁定音頻 | VOD + Live | √ | √（僅限VOD） |
| 302重定向 | VOD + Live | √ | √（僅限VOD） |

### 高級回放功能 {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容類型</strong></td> 
   <td><strong>合肥光源</strong></td> 
   <td><strong>短划線</strong></td> 
  </tr>
  <tr>
   <td>帶偏移的回放</td> 
   <td>實況</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>僅播放音頻</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>特技遊戲 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>平滑特技播放（帶ABR）</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>ID3分析(HLS)/定時元資料(DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>封鎖 </td> 
   <td>VOD + Live</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>即時開啟</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不連續標籤支援(HLS) </li> 
     <li>多週期(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>302重定向靜態</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD）</td> 
  </tr>
  <tr>
   <td>縮略圖清理(Iframe和JPEG)</td> 
   <td>VOD + Live</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>流完整性 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
 </tbody>
</table>

### 核心Ad Insertion功能(CSAI) {#core-ad-insertion-features-csai}

| **功能** | **內容類型** | **合肥光源** | **短划線** |
|---|---|---|---|
| 常規播放，啟用廣告 | VOD + Live | √ | √（僅限VOD預卷） |
| 啟用廣告的FER內容 | 視頻點播 | √ | 不支援 |
| 預設廣告行為 | VOD + Live | √ | √（僅限VOD預卷） |
| 廣2.0/3.0 | VOD + Live | √ | √（僅限VOD預卷） |
| VMAP 1.0 | VOD + Live | √ | √（僅限VOD預卷） |
| MP4廣告 | VOD + Live | √（來自CRS） | √（來自CRS，僅限預卷） |

### 高級Ad Insertion功能(CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>內容類型</strong></td> 
   <td><strong>合肥光源</strong></td> 
   <td><strong>短划線</strong></td> 
  </tr>
  <tr>
   <td>啟用廣告的特技播放</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>僅廣告 </td> 
   <td>視頻點播</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>目標參數</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自定義參數</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自定義廣告行為</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（僅限VOD預卷）</td> 
  </tr>
  <tr>
   <td>自定義廣告標籤</td> 
   <td>實況</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>自定義廣告解析器</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>自由輪自定義Ad解析器</td> 
   <td>視頻點播</td> 
   <td>不支援</td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>C3廣告更換 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>懶惰廣告載入</td> 
   <td>視頻點播</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不連續標籤支援 — SSAI(HLS) </li> 
     <li>多週期(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>夥伴廣告、橫幅廣告和可點擊廣告</td> 
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
   <td>早期廣告退出</td> 
   <td>實況</td> 
   <td>√ </td> 
   <td>不支援</td> 
  </tr>
  <tr>
   <td>基於規則的創意視頻點播+即時優先</td> 
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

| **功能** | **內容類型** | **合肥光源** | **短划線** |
|---|---|---|---|
| AES加密 | VOD + Live | √ | √（僅限VOD） |
| 示例AES加密 | VOD + Live | √ |  |
| 標籤化流 | VOD + Live | √ |  |
| DRM | VOD + Live | 僅限黃金時段DRM(未來：維德文) | 僅Widevine |
| 外部播放(RBOP) | VOD + Live | 僅限黃金時段DRM | 不支援 |
| 許可證輪換 | VOD + Live | 僅限黃金時段DRM | 不支援 |
| 密鑰輪替 | VOD + Live | 僅限黃金時段DRM | 不支援 |

### 整合功能 {#integration-features}

| **功能** | **內容類型** | **合肥光源** | **短划線** |
|---|---|---|---|
| Adobe AnalyticsVHL整合 | VOD + Live | √ | √ |
| 計費 | VOD + Live | √ | 不支援 |

## 不支援的功能 {#features-not-supported}

此版本的TVSDK不支援：

* 廣告封鎖。
* 玩特技的慢動作。
* 尋找MP4內容並逐條播放。
* MP4主內容廣告插入。
* 在廣告播放時查找。
* 播放廣告，只使用音頻介質。

## 已知問題和限制 {#known-issues-and-limitations}

此版本的TVSDK存在以下問題：

* 特定於設備（三星Galaxy Tab 4）的VOD DRM LBA（帶有音頻）崩潰並點擊廣告
* 不為特定內容播放後廣告。
* 將關閉標題設定為CJK語言無效。
* 視頻在視頻點播和直播之間自動退出特技模式。
* VHL — 當我們從偏移量開始內容時，會發送錯誤的心跳呼叫。
* 播放VPAID廣告時，VHL心跳呼叫事件:type:播放廣告丟失。
* 即使選擇adBreakPolicy SKIP時，也會播放預滾廣告。
* 進入「完整」狀態播放器後，使用SKIP adBreakPolicy重新進入「播放」狀態，用於後滾廣告。

沒有視頻，就沒有視區尺寸，沒有視區尺寸，就無法顯示字幕的任何圖形。

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://experienceleague.adobe.com/docs/primetime.html) 的子菜單。
