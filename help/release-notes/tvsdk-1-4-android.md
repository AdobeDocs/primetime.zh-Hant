---
title: TVSDK 1.4 for Android版本注意事項
description: TVSDK 1.4 for Android發行說明說明TVSDK Android 1.4中的新增或變更內容、已解決和已知問題以及裝置問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---


# TVSDK 1.4 for Android發行說明{#tvsdk-for-android-release-notes}

TVSDK 1.4 for Android發行說明說明TVSDK Android 1.4中的新增或變更內容、已解決和已知問題以及裝置問題。

## 新功能{#new-features}

**1.4.43版**

**透過HTTPS安全載入廣告**

Adobe Primetime提供選項，可透過HTTPS要求對黃金時段廣告伺服器和CRS進行首次呼叫。

**alwaysUseAudioOutputLatency(boolean val) in MediaPlayer類別**

設定此參數時，請在音訊時間戳記計算中使用音訊輸出延遲。

它接受布爾參數val。 如果其值為`True`，則客戶端在音頻時間戳計算中使用音頻輸出延遲。

**1.4.42版**

**部分廣告插入：**
在加入廣告中間而不觸發部分觀看廣告的追蹤的電視類體驗。範例：使用者在90秒廣告插播（包含3個30秒廣告）的中間（40秒）加入。 這是分段內第二個廣告的10秒。
* 第二個廣告會在剩餘期間（20秒）播放，接著是第三個廣告。
* 不會引發已播放之部分廣告（第二個廣告）的廣告追蹤器。 只有第三個廣告的追蹤器會被觸發。

**1.4.41版**

無新功能。

**1.4.40版**

無新功能。

>[!NOTE]
>
>如果您使用的版本早於1.4.39，則不需要API變更。

**1.4.39版**

* TVSDK已取得VHL 2.0.1認證，而VHL 2.0.1已取得Nielsen認證。
* Android TVSDK已更新，從新的Akamai主機`primetime-a.akamaihd.net`發出CRS請求。
* 新的主機名稱設定提供CRS資產傳送，可透過HTTP和HTTPS(SSL)進行更大規模的傳送。
* TVSDK支援Android Oreo版本。
* `AdClientFactory`類中添加了一個新函式，以支援註冊多個機會檢測器：

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   這應該會傳回一系列PlacementOpportunityDetector。 現在，您可以註冊多個機會檢測器。 例如，對於早期和退出功能，需要兩個機會檢測器——一個用於廣告插入，另一個用於廣告早期退出。 只有在您已實作自己的AdvertisingFactory（而不使用DefaultAdvertisingfactory）時，才需要實作此新函式。 要獲取現有行為——您需要建立單個Opportunity Detector，如createOpportunityDetector()函式，並放入陣列中並返回：

   ```
   public class MyAdvertisingFactory extends AdvertisingFactory {  
   …  
   @Override  
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
   return opportunityDetectors;  
   } }
   ```

>[!NOTE]
>
>如果您使用的版本早於1.4.39，則不需要API變更。

**1.4.36版**

Android上「內容略過」的錯誤修正。

**1.4.35版**

* **網路廣告資訊**

   TVSDK API現在提供協力廠商VAST回應的其他資訊。 廣告ID、廣告系統和廣告延伸模組都提供在NetworkAdInfo類別中，可透過廣告資產的networkAdInfo屬性存取。 此資訊可用於與其他廣告分析平台整合，例如&#x200B;**Moat Analytics**。

**1.4.31版**

**CRS廣告的多CDN支援**
* 依預設，所有轉碼資產都將裝載在Akamai的Adobe擁有的CDN上。 在最新版本中，Adobe創意重新封裝服務(CRS)提供將轉碼創作元素上傳至客戶指定之多個CDN的功能。
* 新增API至TVSDK，以啟用在未使用預設URL時指定最終的CRS創意URL。 請參閱檔案以瞭解如何使用這些新API。

**1.4.18版**
Primetime Android TVSDK現在支援VPAID 2.0 Javascript創意素材，以提供豐富的串流互動廣告體驗。如需VPAID 2.0的詳細資訊，請參閱[VPAID廣告支援](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)。

**1.4.17版**

AC-3 5.1僅在AmazonFireTV上支援。

**1.4.11版**

* **廣告備援、廣告選擇邏輯中的菊花鏈(Zendesk #3103** For VAST廣告（創意人員），啟用備援規則後，TVSDK會將具有無效MIME類型的廣告視為空廣告，並嘗試在其位置使用備援廣告。您可以設定備援行為的某些方面。

如需詳細資訊，請參閱[VAST和VMAP廣告的廣告後援](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)。

* **視訊心率程式庫(VHL)已更新至1.5版**
   * 能夠以視訊開始和／或視訊／廣告／章節開始傳送中繼資料作為內容資料
   * 網路流量減少——心率平均減少，而且大小較小

**1.4.7版**

* **內部部署個性化支**&#x200B;持支援Adobe個性化伺服器的現場安裝，以定制客戶端的個性化請求，以轉到不同的端點。

**1.4.6版**

* **範例AES加密(需要Flash Player版本17.0.0.134)**現在支援範例型AES加密。

**1.4.2版**

* **視訊心率程式庫(VHL)更新至1.4.0.1版**

   * 新增搭配Adobe Analytics視訊基本工具，搭售其他SDK或播放器的不同分析使用案例的能力。
   * 已移除trackAdBreakStart和trackAdBreakComplete方法來最佳化廣告追蹤。 廣告插播是從trackAdStart和trackAdComplete方法呼叫推斷而得。
   * 追蹤廣告時不再需要播放頭屬性。

* **Nielsen SDK整**&#x200B;合TVSDK現在支援將使用者追蹤資訊傳送至Nielsen SDK，毋需自訂整合。

**1.4.0版**

* **使用替代內容** 取代封鎖訊號在1.4 TVSDK更新中，TVSDK現在也支援針對線性內容進行區域封鎖並返回。TVSDK現在可以並行處理主要和替代的兩個資訊清單檔案，以便監控封鎖訊號，即使替代原始程式設計顯示替代程式設計。

* **移除／取代C3** AdsNow，您不需要額外的準備工作，就能將新廣告動態插入從C3視訊視訊(VOD)資產。TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 此強大的新功能在廣播期間播放即時／線性內容時也很有用，而且會立即下拉以做為隨選內容，而無需適當的時間來「清理」資產。

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，可用來監聽新事件`ITEM_REPLACED`。 每當MediaPlayer上的MediaPlayer項目例項被取代時，就會傳送此事件。 實作此PlaybackEventListener的用戶端應用程式必須實作或覆寫此新方法。
* AdClientFactory在類別中新增了一個新功能，可註冊多個Opportunity Detector:

   ```
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
   
   For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
   
   To override this new function create a single Opportunity Detector, and put into an array and return:
   
   @Override
   
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
   
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
   
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
   
   return opportunityDetectors;
   }
   
   }
   ```

## 1.4 {#tvsdk-changes}的TVSDK變更

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，可用來監聽新事件ITEM_REPLACED。 每當MediaPlayer上的MediaPlayer項目例項被取代時，就會傳送此事件。 實作此PlaybackEventListener的用戶端應用程式必須實作或覆寫此新方法。

* AdClientFactory在類別中新增了一個新功能，可註冊多個Opportunity Detector:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

例如，對於早期廣告退出功能，您需要兩個機會檢測器——一個用於廣告插入，另一個用於廣告早期退出。

要覆蓋此新函式，請建立單個Opportunity Detector ，並放入陣列中並返回：

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4 {#device-certification-and-support-in}中的裝置認證與支援

>[!NOTE]
>
>TVSDK支援下列功能：**not**:
>
>* 在任何平台或版本上都能執行慢動作。
>* 即時戲法遊戲。


**1.4.43版**

TVSDK 1.4.43已通過Android裝置的認證，其Android裝置具有Android 6.0.1/ 7.0和8.1(Oreo)。

* **1.4.23版：**

   * TVSDK 1.4.23已通過Android N裝置的認證。

* **1.4.18版：**

   * Primetime已獲得AmazonFire TV認證。
   * VPAID 2.0僅在Android 4.0及以上版本的裝置上受支援。

## 已解決1.4 {#resolved-issues-in}中的問題

>[!NOTE]
>
>強烈建議所有使用CRS的TVSDK客戶升級至iOS和Android上的TVSDK 1.4.39或最新版本。 此升級是現有應用程式實作的下載取代。 升級後，請在Proxy工具（例如Charles）中檢查CRS創意URL要求，以確認路徑中的版本是否反映3.1版。例如：
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**1.4.43版**

* 票證#27143 —— 無法在FireTV裝置上播放5.1音軌

   * TVSDK現在可在FireTV裝置上播放AC3音訊。 播放一律採用立體聲。

* 票證#33902 —— 透過HTTPS安全廣告傳送

   * Adobe Primetime提供選項，可要求在https上首次呼叫黃金時段廣告伺服器和CRS。

* 票證#34493 —— 藍芽音頻延遲

   * 在MediaPlayer類別中新增`alwaysUseAudioOutputLatency`，當設定時，會導致在音訊時間戳記計算中使用音訊輸出延遲。

* 票證#34949 —— 整合的新版視訊心率程式庫(VHL)。

**1.4.42版(1791)**

* Zendesk #33719:FireTV 4k可調式位元速率會緩慢縮放。 已新增對FireTV 4K裝置的ABR支援。
* Zendesk #3338: resetDRM會清除應用程式的所有資料。  已處理非TVSDK執行緒中的例外導致TVSDK作業佇列填滿的額外案例。

**1.4.41版(1776)**

* Zendesk #33002 - Fire TV上TVSDK的附屬資產資料。 實作新類別AdBannerAsset，其會將使用者資料傳回為清單&lt;AdBannerAsset>，而AdAsset::id現在是字串，而非長字串。
* Zendesk #32821 - Android Primetime播放器遇到WWE的簡報時間戳記(PTS)時會凍結。 這個問題已修正。
* Zendesk #33572 - VideoAnalyticsProvider廣告開始當機。 使用VHL+Nielsen聯合SDK版VideoHeartbeat.jar的正確組合來修正此問題。
* Zendesk #3355 - Fire TV:拖曳15秒。 TVSDK方面沒有任何修正，客戶在其「終端」和「第三方」驗證此項修正。

**1.4.40版(1764)**

* Zendesk #33068 —— 新裝置上的Amazon同步對嘴問題。 此版本已修正同步對嘴問題。
* Zendesk #32215 - Android TVSDK 1.4.38安全性問題`[Hotlist]`。 已更新至最新的OpenSSL-1.1.0和curl-7.55.1。
* Zendesk #32920 —— 廣告插播內的空白畫面，無廣告插播完成。 修正VPAID容器可能陷入擱置狀態並處理Facebook VPAID廣告通常在單一\&amp;lt;AdParameters\&amp;gt中傳回多個CDATA區塊的問題；巨型節點。

**1.4.39版(1744)**

* Zendesk #28976 —— 授權要求需要超過一秒的時間。 當使用POST的DRM授權要求呼叫正在執行時，Curl會新增額外「預期：100-continue」標題。 已移除TVSDK中的「預期：」標題。
* Zendesk #27707 - CSAI環境不支援CUE IN標籤，以便提前返回或返回內容。 為多個機會生成器提供支援。

**1.4.38版(1722)**

* Zendesk #21590 —— 最新原始建置中的視訊效能與追蹤

在TVSDK中整合併認證VHL 2.0，以降低API的複雜性，以降低VideoHeartbeatsLibrary實作中的障礙。

* Zendesk #29688 —— 支援Android O Beta版客戶。

新Android測試版的TVSDK支援。

**1.4.36版(1713)**

* Zendesk #27392 - Android上的內容略過

為了容許解密，Android TVSDK錯誤地將非iframe內容的位元組範圍擴大16位元組。 Iframe串流需要加寬，但非iframe串流則不需要加寬。

**1.4.34版(1702)**

* Zendesk #27638 - Leak in cURL INet object

Posix cURL INet物件在保持cURL連線中使用的共用管理員和DNS快取時，會洩漏。

此問題已解決，方法是從INet剖析器刪除Posix cURL INet物件。

**1.4.33版(1694)**

* **OpenSSL程式庫**

OpenSSL程式庫已更新為OpenSSL 1.0.2j版。

* Zendesk #21701 —— 傳送1401 CRS要求的原始創意URL，而非標準化的URL。
傳送原始的創意URL可解決此問題。

* Zendesk #25023 —— 長視訊播放：視訊凍結，螢幕閃爍
此問題已透過為CenturyLink機上盒裝置設定最大視訊格式尺寸來解決。

* Zendesk #27460 —— 新的Akamai帳戶無法處理POSTcdn請求。
已更新程式碼，讓`cdn.auditude.com`廣告要求成為GET而非POST。

* Zendesk #28245 —— 當應用程式從背景移至前景時，播放狀態未正確通知
此問題已解決，方法是在應用程式返回前景時，正確還原播放狀態以播放或暫停。

**1.4.32版(1682)**

* Zendesk #25779 - TVSDK發現的安全性弱點
當WebView中啟用JavaScript時，Android 4.2和更低版本會出現安全性弱點。 已停用執行OS 4.2或更低版本之裝置的WebView by TVSDK。 這會停用這些裝置上TVSDK中的VPAID廣告使用。

* Zendesk #26890 —— 處理參考的「螢幕」狀態問題（開／關） 播放器
當Adobe視訊引擎(AVE)從「暫停」狀態恢復時，DefaultMediaPlayer不會更新其狀態。 因此，即使AVE處於「播放」狀態，DefaultMediaPlayer仍然處於「暫停」狀態。 此問題已解決，即使DefaultMediaPlayer的目前狀態為SUSPENDED，從AVE接收PLAY狀態時，也將DefaultMediaPlayer狀態設為PLAYING。

**1.4.31版(1675)**

* Zendesk #21974 —— 由空對象引起的例外
   * AdIndex在null時很少增加。 這可能是因為前段adBreak收到錯誤的API呼叫所致。 修正資料類型，以避免此類例外

* Zendesk #24714 —— 關閉無關的日誌記錄
   * 更新TVSDK以關閉無關的記錄

* Zendesk #24488 - Fire TV上的AV同步問題
   * 通過改進AV解碼器線程的處理來修正。 具體地，每當輸入或輸出幀隊列被修改時，就運行特定於幀的內容類型的解碼器線程。

* Zendesk #26551 —— 修復CRS故障
   * 當請求是HEAD(http head)時，我們不需要讀取內容，因為它是空的。 雖然可以嘗試讀取，但舊版Android(4.0.x)在呼叫read()時掛起，而較新的Android在呼叫read()時會傳回正確值(-1)。 因此，將程式碼變更為不讀取「head」的內容

* Zendesk #26696訪問TrickPlayManager時空指針異常
   * 修正方法：在使用TrickPlayManager物件之前，先檢查TrickPlayManager物件是否為null。

**1.4.30版(1659)**

* Zendesk #22675資產持續時間未針對即時／線性串流進行更新
此問題已解決，方法是在PTVideoAnalyticsTrackingMetadata中提供新的API assetDuration，以提供即時和線性串流的資產持續時間。

* Zendesk #25853切換頻道時TVSDK中的記憶體洩漏
MediaPlayer重設或釋放檔案讀取緩衝區時，檔案讀取緩衝區洩漏的問題已解決。

**1.4.29版(1653)**

* Zendesk #21200 —— 當應用程式在背景時，播放器無法從暫停狀態復原
當播放器在串流切換被信號通知後被暫停時，解析度允許播放器在從暫停狀態恢復播放器時執行串流切換，而不是還原到先前位置。

* Zendesk #23412 —— 如果您在廣告插播的最後3秒內點選任何廣告，播放器會卡在黑色方塊上
此問題與Zendesk #21200的問題相同。

* Zendesk #23616 —— 跳過廣告片段未來追求太遠
視廣告插入類型（插入／取代）而定，TVSDK會決定廣告持續時間是否用於計算以決定廣告插入端點。

* Zendesk #25078 - Android TV STB上的TVSDK DRM記憶體洩漏
DRM適配器對象的記憶體洩漏已經定位並固定。

* Zendesk #25067 - VideoEngineTimeline當機
發生此情況是因為物件未正確清理，而事件是在物件毀損後呼叫。 通過添加檢查來防止空例外，問題已得到解決。

* Zendesk #25352 —— 設定自訂HTTP標題
此問題已透過在TVSDK的允許清單中新增自訂標題來解決。

* Zendesk #25617 —— 即時串流PTS變換導致播放器中斷和記憶體損毀
當區段中間發生變換時，在BracketedHTTPStreamer中新增PTS變換處理，以解決此問題。

**1.4.28版(1637)**

* Zendesk #23618 —— 在咨詢廣告政策之前，會引發廣告中斷事件
此問題已解決，方法是在由於adInpressition而略過廣告時，不觸發AD_BREAK_START和AD_START事件。 AD_BREAK_KLIPPED事件會改為傳送。

**1.4.27版(1631)**

* Zendesk #23174 —— 調整視訊大小時的效能問題
此問題已透過驗證新的API MediaPlayerView.setSurfaceFixedSize來解決，此API可讓TVSDK從MediaPlayerView存取SurfaceHolder.setFixedSize()。

* Zendesk #24450 - TVSDK發出重複的廣告要求
此問題發生在經過的時間轉換為長時間而非雙倍時，且此問題已修正。

**1.4.26版(1627)**

* Zendesk #21436 - OpenSSL程式庫更新至1.0.2h版將OpenSSL程式庫更新至OpenSSL 1.0.2h版
* Zendesk #23825 —— 回呼中未包含Cookie，因為提供Android Cookie支援。

**1.4.25版(1620)**

* Zendesk #22900 —— 即時Adobe PrimetimeDRM串流未在Android參考播放器上播放
記憶體分配問題已修正。
* Zendesk #23176 —— 當應用程式嘗試播放VPAID廣告時當機
當機是因為應用程式未建立自訂廣告檢視來轉譯VPAID廣告。 當沒有自訂廣告檢視時，會忽略廣告伺服器回應中的VPAID廣告，以解決此問題。

* Zendesk #23153 - SampleAES DRM串流——在TVSDK參考播放器中播放停止
此問題與Zendesk #22900相同。

**1.4.24版(1612)**

* Zendesk #20784 - Analytics:觸發內容完成即時視訊轉場
此問題已解決，方法是新增API(trackVideoComplete)，以手動觸發即時／線性視訊追蹤工作階段中的內容完成。

* Zendesk #21977 VideoEngineplaceAdBreak/acceptAd操作期間時間軸當機
   * 在此問題中，已更新下列程式庫：
      * 4.10.0版的AdobeMobile程式庫
      * 1.5.6版的VHL程式庫
      * VHL-Nielsen資料庫至1.6.7版

在將廣告新增至接受的廣告清單之前，新增空值檢查，以解決此問題。

* Zendesk #22313帶Amilogic晶片集的STB的位元速率不會超過1.2M
此問題已解決，方法是預先載入媒體轉碼器功能，並停用Amilogic晶片集裝置的順暢切換。

* Zendesk #19520範例AES HLS資產未在TVSDK播放器中播放
此問題已通過處理用於樣本AES加密的HLS流的多個PMT描述符來解決。

**1.4.23版(1602)**

* Zendesk #18852 —— 根據CRS規則更新創意選擇邏輯
此問題已透過新增JSON設定檔案來指定創意選擇的優先順序來解決。

* Zendesk #20861 - Android N
此版本移除直接使用在Android N上執行之應用程式無法再存取的Android平台原生程式庫，以支援Android N。

* Zendesk #21018 - Android N當機
與ZD# 20861相同的解析度。

* Zendesk #21266 - VideoEngineAdapter在Invalid_Key錯誤時當機
Invalid_Key錯誤不包含AVE的說明，因此剖析文字會產生NPE。 在剖析說明之前，新增onError期間說明的空值檢查，以解決此問題。

* Zendesk #22286 —— 本機庫正在分配記憶體讀取密鑰／碎片，導致崩潰
嘗試同時載入具有多個鍵的資訊清單時，在Android上發生的當機問題已經修正。

**1.4.22版(1581)**

* Zendesk #17236 —— 使用DRM的HLS視訊不可靠的播放時間
LBA串流的時間跳轉已修正，其中音訊區段開始時間與視訊區段開始時間不符。

* Zendesk #17680 - Selevision Andredo包裝盒上的視訊播放已凍結
當將視訊幀從輸出緩衝區出隊時，此裝置上的視訊解碼器有時會傳回顯著的輸出時間跳變，而此輸出時間戳記仍維持高。 此問題已解決，因為傳回不支援的*視訊設定檔*&#x200B;錯誤不會強制播放器重試相同的設定檔或選擇不同的設定檔。

* Zendesk #19074 - FFWD和REW特技播放期間視訊凍結
此問題已解決，方法是新增警告TRICKPLAY_ENDED_DUE_TO_ERROR，通知應用程式trickplay已退出，且視訊因無法復原的錯誤而暫停。

* Zendesk #19574 - TVSDK不會傳回DRM或非DRM內容的M3U8回應資料
此問題已透過下列方式解決：

* Zendesk #19986 —— 某些裝置（例如Android TV）的OP行為中斷
* 將FILE_NOT_FOUND錯誤添加到條件。
* 當錯誤來自&#x200B;*檔案找不到*錯誤時，若有回應，請將URL和回應與錯誤說明分開。
由NVidia防護罩OP支援所引入的邏輯錯誤已修正。 在非NVidia防護板設備上，即使顯示類型未知，也要信任顯示安全標誌。

* Zendesk #20549 —— 處理過時的播放清單。 如果先前的擷取未收到新區段，將即時資訊清單更新之間的間隔縮短至預期區段持續時間的一半，就可解決此問題。

* Zendesk #20742 —— 在FireTV上播放即時內容時，記憶體使用量似乎持續增加。當機是由JNI物件參考表達到限制所致。 此問題已解決，方法是刪除在解碼器重新啟動期間建立之MediaFormat物件的參考。

* Zendesk #21125 —— 提早從即時／線性廣告插播(CSAI)返回。 新增功能，讓玩家在廣告插播期間，如果玩家使用機會插播偵測器，在廣告提示中註冊剪接，就可返回主要內容。

* Zendesk #21334 - TVSDK廣告要求第三方廣告要求的逾時值。 adRequestTimeout設定已新增至AdvertisingMetadata，可啟用廣告呼叫的全域逾時。

**1.4.21版(1566)**

* Zendesk #17781 - ADB螢幕擷取不再有效
此問題已借由新增DefaultMediaPlayer.create(Context context, boolean secureSurface)API來解決，API允許螢幕擷取。
若要允許螢幕擷取，請為secureSurface傳遞false。
重要：強烈建議您不要在生產設定中啟用此螢幕擷取功能。

* Zendesk #19074 - FFWD和REW特技播放期間視訊凍結
下列trickPlay可能會凍結在playback中時發生的問題已解決：

* Zendesk #19532 —— 關閉標題顯示不正常
   * FHS會開始逐字逐句播放，但第一個iframe區段中沒有影格。
   * 在下載iframe區段時，如果FHS點擊錯誤條件，則會退出特效播放並暫停播放。
   * 此外，MediaCodec實作會在要求清除所有輸入／輸出緩衝區時，等待輸入佇列的可用性。
此問題已解決，方法是反轉WebVTT提示的順序，讓多個重疊提示看起來像是「向上捲動」。

* Zendesk #19574 - TVSDK不會傳回DRM或非DRM內容的M3U8回應資料
在PTMediaPlayerItem.prepareToPlay中初始載入manifest檔案時，如果載入失敗，TVSDK不會向應用程式報告失敗回應的正文。
此問題已解決，因為TVSDK會將失敗回應報告為應用程式的錯誤。

* Zendesk #19701 —— 使用SAP/不連續播放凍結
已解決當音訊和視訊在不連續處未對齊時播放器凍結的問題。

* 錯誤#PTPLAY-11162 —— 已解決1.0.2f版的OpenSSL程式庫更新。

**1.4.20版(1546)**

* Zendesk #17384 —— 功能要求：AAC播放的ID3中繼資料支援
從1.4.20版開始，適用於Android的TVSDK支援AAC媒體中的ID3標籤。

* Zendesk #18358 —— 播放器在位元速率切換時會因不同步中斷而凍結
此問題已透過正確處理ABR拼接邊緣案例而解決。

* Zendesk #19232 —— 使用TVSDK 1.4.18的應用程式在舊版AmazonOS 4上的行為異常
此問題已解決，方法是移除TVSDK播放器初始化程式中隱藏的網頁檢視建立，以避免與不支援Android Webview的裝置產生衝突。

* Zendesk #19585 —— 當可調式位元速率轉換發生時，慢動作播放。
在ABR切換期間，如果新配置檔案的音頻採樣速率與當前配置檔案不同，則回放會變得快速或慢速。 這是因為影片簡報人員未收到音訊格式變更的通知。
此問題已解決，方法是確定通知標幟已設定在正確的位置。

* Zendesk #19683 - SAP DAI回放——幾秒鐘內無音頻。
在TVSDK邏輯中，若干情況下，比較兩個轉譯區段的時間戳記時，會使用RENDITION_TIMEOUT_THRESHOLD作為可接受的值範圍，因為時間戳記無法總是與0毫秒的差值相符。 如果間隙在RENDITION_TIMEOUT_THRESHOLD範圍內，則假設為匹配。

RENDITION_TIMEOUT_THRESHOLD已設為100ms，但發現它不足以用於某些流。 將RENDITION_TIMEOUT_THRESHOLD增加到200毫秒，解決此問題。

* Zendesk #19699 - TVSDK無法在VTT子標題軌道之間切換
此問題已解決：在追蹤變更時，讓播放器轉儲並重新載入資訊清單，並修正影響雙位元組WebVTT標題追蹤名稱的UTF8字串轉換問題。

* Zendesk #19717 - CC選項顯示問題
此問題已透過正確處理Unicode字串而解決。

* Zendesk #19910 —— 未檢測到TIT2 ID3標籤
此問題已解決，因為它提供更完整的ID3 v2.4字串編碼支援以及ID3 v2.3支援。

* Zendesk #20135 - TVSDK正在針對VOD內容觸發多個onComplete。
此問題已解決，方法是將post_roll_compelete事件偵聽器新增至正確位置，而非在狀態變更事件的完整案例。

**1.4.19版(1521)**

* Zendesk #4180 - TVSDK未強制執行HDCP。
   * 這是此票證的部分修正，僅解決NVidia防護板設備的問題。
您必須使用Nvidia Shield中正確實作的HDCP偵測API，以動態追蹤HDCP狀態。

* Zendesk #18358 - TVSDK會在位元速率切換時停止同步中斷。
   * 通過添加新警告來檢測PTS不連續性，並強制PTS檢查重做對每個ABR交換機的正確段的搜索，解決了此問題。
若要修正凍結，對mediaPlayer.setCustomConfiguration方法的呼叫應包含forcePTSCheckForABR做為引數。

* Zendesk #19038 - Asus Zenpad 10上沒有即時串流。

   此問題已借由預先載入媒體codec資訊來解決，因此您不會在執行時期查詢函式。

* 下列問題與Zendesk #19038相同：
   * Zendesk #19483 - TVSDK在英特爾平台上當機。
   * Zendesk #19171 —— 在Android 5.0的Asus Memo Pad 7上當機。

**1.4.18版(1503)**

* Zendesk #3324 - Primetime廣告報告不會在VMAP中沒有廣告媒體時追蹤廣告插播。
當廣告插播是空的時，廣告插播開始和完成追蹤事件都未被Ping通。 此問題已解決，方法是在空廣告插播（例如VMAP AdBreak）上傳送廣告插播開始ping，並提供有效的AdSource點頭。

* Zendesk #18229 - MediaPlayer.reset()呼叫後會忽略SetCCVisibility(VISIBLE)
此問題已借由新增setCCVisibility(Visibility.INVISIBLE)而解決；至MediaPlayer類別中的reset()函式。

* Zendesk #18328 —— 針對60FPS內容，在AmazonFire TV第2代裝置上掉格問題
此問題已解決，方法是將編碼的FPS套用至睡眠時間決策，並使用更好的編碼的FPS預測邏輯。

**1.4.17版(1472)**

* Zendesk #2231 —— 擷取MediaPlayerNotification中無法使用的資訊清單時傳回錯誤
此問題已解決，方法是在出現解析錯誤時加入資訊清單的回應本體。

* Zendesk #17703 - VideoEngineView無法防止視訊播放期間的螢幕擷取
setSecure方法自API 17起就已推出，但由於API 17涵蓋4.2、4.2.1和4.2.2，因此不知道哪個方法會擲出異常，或是否是裝置特定。 此問題已透過將VideoEngineView.setSecure封裝在try catch子句中而解決。

* Zendesk #17919 —— 內容搜尋導致心率錯誤
由於預先滾動後開始搜尋時產生的心率呼叫，導致無效輸入資料位置錯誤。 此問題已解決。

**1.4.16a** (1454a)

* Zendesk #18215 —— 某些AES串流無法載入。
此問題已解決，方法是在載入AES金鑰前先檢查描述檔DRM中繼資料大小。

**1.4.16版(1454)**

* Zendesk #3875 - Tab S在播放期間當機
回復OKHTTP對CRS Auditude的依賴性，因為TVSDK現在直接使用httpurlconnection而非curl。 在進行任何其他JNI呼叫前，清除例外即可解決此問題。

* Zendesk #4487 —— 追蹤線性內容頻道
此問題已解決，允許線上性串流播放工作階段期間重新初始化視訊心率追蹤器。

* Zendesk #17919 - Android —— 內容搜尋導致心率錯誤
已解決當章節中有搜尋時，心率處於錯誤狀態的問題。

* Zendesk #18053 -Adobe Primetime在棉花糖上當機
當TVSDK程式庫使用進行YUV -> RGB色彩轉換的neon程式碼時，TVSDK會在Android M OS上當機。 此問題已解決，方法是使用非霓虹版的程式碼更新造成此問題的函式。

* Zendesk #18072 - Android M —— 應用程式當機
在檢查描述檔和層級是否受支援時，呼叫MediaCodecList和MediaCodecInfo API時會發生當機。 此問題已解決，方法是提前載入所有的codec資訊，以避免僅在需要codec資訊時呼叫這些API。

* Zendesk #18074 —— 阿拉伯文字幕無法用於Nexus with Android 6.0
此問題已透過提供Android的CTS字型對應支援來解決。

**1.4.15版更新(1438)**

* Zendesk #17437 —— 某些AES串流的VOD內容啟動的長延遲。
若要解決此問題，如果資訊清單中列出多個索引鍵，請並行下載所有AES索引鍵。

**1.4.15版(1435)**

* Zendesk #4278 —— 當可調式位元速率變更(ABR)時，Android裝置上盒上的故障。
修正之處是，新增支援最新Android媒體轉碼器的順暢ABR切換。

* Zendesk #17063 —— 呼叫mediaPlayer.reset()會造成視訊引擎重設錯誤。
修正是，在分派ErrorEvents時，會包含VideoEngineExceptions的原始MediaErrorCode。

* Zendesk #17130 —— 在變更FireTV上顯示的位元速率時，會短暫但引人注目地暫停。
（與上文第4278條相同）修正之處是新增支援順暢的ABR切換與最新的Android媒體轉碼器。

* Zendesk #17666 —— 繼續內容時的其他廣告標籤、非預期或無廣告。
修正針對隨選視訊(VOD)內容進行prepareToPlay時，初始搜尋會在本機時間而非虛擬時間執行的問題。

* Zendesk #17437 —— 某些AES串流的VOD內容啟動的長延遲。
修正是當資訊清單中列出多個索引鍵時，並行下載所有AES索引鍵。

* Zendesk #17851 - Android TV - ABR期間的黑色影格
修正是指定KEY_MAX_WIDTH和KEY_MAX_HEIGHT以啟用自適應播放。

**1.4.14版(1415)**

* Zendesk #3875 - Tab S在播放期間當機。
需要額外的修正來防止當機。

* Zendesk #17245 - Fallback on Android TV is not function.
已修正在啟用備援時，而VMAP回應有空廣告插播時，播放會暫停的其他問題。

**1.4.14版(1412)**

* Zendesk #17245 - Android TV後援功能無法運作。
已移除停用備援廣告創意重新封裝的限制。

**1.4.13版(1388)**

* Zendesk #3502 —— 廣告插播期間基於HLS客戶端的故障切換支援
在廣告中斷期間更新即時描述檔錯誤時，允許容錯移轉至主資訊清單。

* Zendesk #3875 - Tab S在播放期間當機
若要解決HttpUrlConnection和cURLm之間的衝突，請使用協力廠商程式庫。

* Zendesk #4450 —— 問題為內容解析器中的單個位置設定自定義元資料
將setter添加到Opportunity設定中。

**1.4.12版(1388)**

* Zendesk #2751 - CSAI和CRS |增強：處理特定媒體檔案URL中的動態元素。
更新Creative重新封裝服務，以使用動態創意URL正確處理廣告。

* Zendesk #3965 —— 從滴答作業切換回正常播放，在開始播放前會先跳一點。
   * 修正包含TVSDK，可傳回比率變更前的時間，直到所有變數更新為止，而不是嘗試計算GetStreamTime。
   * 修正在串流結尾處變更特技播放速度時發生當機的問題。
   * 修正特技播放期間的目前時間計算。

* Zendesk #3978 -8x16x的Trickplay經常凍結。
   * 請務必以最低的位元速率來挑選特技播放設定檔，以避免持續的緩衝。
   * 增加跳過影格間隔，以提高特技播放率。
   * 修正在特技播放期間達到目標長度後，緩衝區持續增長的問題。

* Zendesk #3992 —— 額外的特技播放速度。
TrickPlay已更新，接受高於16倍的速率；+/- 32、+/-64和+/-128現在也允許使用。

* Zendesk #4007 —— 將GEOB物件解譯為時間軸中繼資料（Android與Web）的一部分。
已新增setByteArray和getByteArray API。

* PTPLAY-7301 —— 從隨機接入點開始立即啟動。
「立即啟動」已更新，允許非零起始點。

**1.4.11版(1363)**

* Zendesk #2076 —— 在Android 4.0.3的Motorola Xoom上播放視訊時經常發生斷斷鍵
已新增裝置以允許清單，以防止其嘗試播放高描述檔內容。

* Zendesk #2197 - `[Ads]`追蹤廣告錯誤
dispatch OperationFailedEvent，含警告通知。

* Zendesk #3304 —— 未填充VAST 3.0 `[ERRORCODE]`宏
   * 如果內嵌廣告的創意不佳，則會公開錯誤代碼400。
   * `[ERRORCODE]` 巨集將是URL編碼

**1.4.10版(1354)**

* Zendesk #2941 —— 即時資產在可見範圍內沒有「0」
以前，在尋找即時串流的開頭時有3個區段緩衝區，現在可以尋找即時串流的開始（即第一個區段的開始）。

* Zendesk #3169 —— 更新參考播放器與Adobe Analytics整合參考播放器參考播放器已以Adobe Analytics資料庫更新為例進行植入。
* Zendesk #3299 —— 無法解釋的特技遊戲行為
   * 已修正在停止特技播放後，可能需要數秒（有時需要25秒以上）才能返回播放狀態的錯誤。
   * 已修正在相同媒體上再次叫用特技播放，可能導致串流在目前時間凍結的錯誤。
* Zendesk #3433 - Android和Flash-字幕問題

GetLine for WebVTT不會尊重&lt;CR>&lt;LF>調整的封包長度；最後一個標題可能包含先前標題中的字元。

* PTPLAY-6243 —— 增強參考播放器，以擷取除錯資訊

Android範例參考播放器已增強，提供開啟除錯記錄檔並以電子郵件傳送結果的選項。 此選項位於參考播放器的「記錄」功能表下。

**1.4.9版(1332)**

* Zendesk #2649 —— 在初始緩衝區滿之前，緩衝區完成

在搜尋後，視訊引擎在視訊簡報人員準備好播放之前，將狀態設定為「播放」的可能案例。 發生於尋道前緩衝區狀態高時。 透過通知視訊引擎緩衝區狀態不足來修正。 由於視訊引擎緩衝區狀態低，呼叫「播放」會導致狀態變更為BUFFERING，而非PLAYING。 當狀態變更為「播放」時，播放會繼續。

* Zendesk #2846 —— 增強請求：提供為Auditude程式庫所呼叫設定不同使用者代理字串的功能

已新增新API，以設定廣告相關呼叫的使用者代理，auditudeSettings.setUserAgent(&quot;user/agent&quot;)。 如果未設定使用者代理，則會使用預設值。 這只會影響廣告相關呼叫的使用者代理，媒體呼叫的使用者代理不會變更，即&quot;Adobe Primetime&quot;+&lt;預設使用者代理>。

**1.4.8版(1324)**

* Zendesk #1218 - 106000.33本機錯誤……如果在FracteredHTTPStreamer::ThreadParseManifest()中載入manifest時失敗，請檢查URL網域是否為localhost，如果是，請將網域變更為127.0.0.1，然後重新叫用ThreadParseManifest。
* Zendesk #3072 —— 自動切換至較低的位元速率。 將緩衝區長度計算更改為跳過零PTS有效負載。
* Zendesk #3168 - WebVTT字幕僅顯示前10秒。
* Zendesk #3193 —— 在TVSDK中請求設定檔變更API，已新增PlaybackEventListener.onProfileChanged()。

**1.4.7版(1311)**

* Zendesk #2197 —— 追蹤廣告錯誤。 新增資產通知無法載入資訊清單
* Zendesk #2575 - PSDK會在視訊之前忽略MARK自訂串流內廣告
* Zendesk #2719 - Win Death with auditude ads, cifed beacon tracking when redirected to relative url in auditude plugin
* Zendesk #2760 - TrickPlay模式期間忽略的DINSTRUCTION標籤
* Zendesk #2805 —— 播放開始時播放器崩潰，與Zendesk #2719相同的修正
* Zendesk #2817 - Android player —— 播放器有時候會掛起並停止播放，修正方法是將解碼緩衝區從2.0延伸至3.0秒
* Zendesk #2839 -Adobe PrimetimePSDK是否支援ARMv8晶片組？已新增Galaxy S6的當機修正。
* Zendesk #2885 - Auditude當機播放，與Zendesk #2719相同的修正
* Zendesk #2895 —— 在播放10分鐘後始終如一地出現即時HLS故障
* Zendesk #2925 —— 當將封包排入輸入佇列時，在某些裝置上，當我們將封包排入輸入佇列時，有關Android dev組建(1.4.5)的回饋，如果PTS為負數，則解碼器會進入奇怪的狀態，我們總會為未來封包取得負數輸出PTS。 如果輸入PTS為負值，則此修正會將其設為零，以避免此問題。
* PTPLAY-4645 —— 關閉openssl中的RC4密碼支援。 已知RC4利用漏洞。 這表示如果嘗試連接僅支援RC4的伺服器，將失敗。

**1.4.6版(1282)**

* Zendesk #2192 —— 位元速率在較差的網路狀況下並不總是較低，而是透過移除快速的交換機實施來修正。
* Zendesk #2631 - Android上的阿拉伯文字幕：多行文字會被切斷，並透過調整阿拉伯文字型的字型大小來修正。
* Zendesk #2844 - Buffering on Note 4 and Fragment download time is not accure.

此問題已經修正，將視訊區段下載之間的延遲加入頻寬計算，並讓下載時間計算邏輯使用完整的請求週期時間。

* Zendesk #2908 —— 阿拉伯文字幕在Nexust 5、6和7上無法運作，已針對阿拉伯文指令碼新增2種備援字型來修正。
* PTPLAY-4627 —— 將Nielson應用程式sdk更新至1.2.3.7版
* PTPLAY-5084 —— 即時主資訊清單更新容錯移轉支援

**1.4.5版(1248)**

* Zendesk #1757 —— 針對某些視訊位元速率設定檔，僅播放音訊或播放器當機，Nexus 4和Nexus 7當機已修正
* Zendesk #2072 - TimedMetadata for AdEvent不包含完整的URL，僅「http」
* Zendesk #2192 —— 在較差的網路條件下，位元速率不總是較低
* Zendesk #2256 —— 存取主播放清單，更新PSDK，為主播放清單上的訂閱標籤分派timedMetadata事件。
* Zendesk #2269 —— 使用WebVTT，螢幕上同時出現兩種不同的字幕語言
* Zendesk #2417 —— 播放器嘗試在播放開始前下載字幕，WebVTT使用錯誤的區段編號變數來比對區段編號。 只有區段索引從零開始的媒體才會顯示錯誤。
* Zendesk #2470 —— 當位元速率變更在暫停後發生時，PSDK不會從SUSPENDED狀態返回。 在RestoreGPUResource（從暫停狀態恢復播放器）呼叫智慧搜尋以及之前偵測到串流切換的特殊情況下，智慧搜尋無法完成，並導致持續緩衝。
* Zendesk #2451 —— 隱藏字幕「底部內嵌」，在字幕代碼中新增「bottomInset」參數
* Zendesk #2480 —— 停用HTTP 302重新導向最佳化，新增對設定useRedirectedUrl屬性的支援
* Zendesk #2486 —— 第三方信標
* Zendesk #2547 —— 阿拉伯文字幕：文本應對齊右對齊

**1.4.4版(1195)**

* Zendesk #1158 - Huawei Valiant上播放失敗(Y301A1)
* Zendesk #1709 —— 不正確的媒體大小和延伸視訊
* Zendesk #1757 —— 僅在使用相同spa/pps資料的串流之間進行設定檔切換後播放音訊
* Zendesk #2095 - HTTP 307狀態（重新導向）導致Adobe播放器停止播放
* Zendesk #2126 —— 最後一個ADEVENT的TimedMetaData事件遺失，最後一個區段之後存在的已訂閱標籤未從AVE報告給PSDK
* Zendesk #2227 - VideoEngine nativeReset和nativePause中的鎖定
* 錯誤#3921755 - OpenSSL程式庫更新至1.0.1L版

**1.4.3版(1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 —— 隱藏字幕開啟和關閉
* PTPLAY-1818 —— 倒轉特技播放會停在廣告上，而不是繞過廣告
* PTPLAY-2736 —— 當具有WebVTT標題的串流播放完成時，畫面上會顯示先前顯示的WebVTT標題
* PTPLAY-3773 —— 當在廣告位置後啟動串流播放時，不會播放中間廣告

**1.4.2版**

* Zendesk #1561 —— 黃金時段基於HLS客戶端的故障切換支援。 將使用程式日期時間解決故障轉移
* Zendesk #1590 - LoadInfo.MediaDuration一律為0（非僅音訊修正）
* Zendesk #1626 - Player中可能的記憶體洩漏。 不是實際的記憶體洩漏，問題是NotificationHistory儲存最近1000則通知，這個問題已降為100。
* Zendesk #2192 —— 在較差的網路條件下，位元速率不總是較低

**1.4.1版(1121)**

* Zendesk #1951 - 4.0.x裝置上VideoEngine.nativeReset()鎖定
* Zendesk #2064 —— 特定Intel架構Android裝置上的原生當機SIGSEGV
* Zendesk #2075 - 4.0.x裝置上VideoEngine.nativeReleaseGPUResource的鎖定
注意：此版本是支援Android 5.0(Lollipop)的***必要***
* Zendesk #1513 - Android Lollipop支援
* Zendesk #1709 —— 不正確的媒體大小和延伸視訊
* Zendesk #1871 —— 使用WebVTT標題檢視即時串流時，WebVTT標題偶爾會消失，然後重新出現
* Zendesk #1996 - PSDK 1.4.0中未顯示時間軸標籤
* Zendesk #2046 —— 使用PSDK 1.4.1.1113時發生當機，修正即時串流當無廣告從auditude傳回時的當機問題
* 錯誤#3769657 —— 將捲曲版本更新為7.38.0
* PTPLAY-1575 —— 當ABR播放以僅音訊串流開始，然後切換至音訊／視訊串流時，視訊不會呈現，而音訊會持續
* PTPLAY-2499 —— 更新至OpenSSL至1.0.1j版以解決最近的弱點
* PTPLAY-2632 —— 在Android Lollipop上完成中段廣告後，視訊無法復原
* PTPLAY-2678 —— 在Android Lollipop的即時壽命測試期間視訊停止

**1.4.0版**

* Zendesk #1024 —— 透過資訊清單從串流移除廣告的功能
* Zendesk #1293 —— 隱藏字幕音軌選擇問題。
* Zendesk #1590 - LoadInfo.MediaDuration始終為0,mediaDuration現在顯示正確的值。
* Zendesk #1629 —— 播放器／應用程式在Galaxy S4廣告播放結束時當機
* Zendesk #1674 - ClosedCaption未顯示，當0x03 ETX代碼遺失時，708標題顯示正確。
* PTPLAY-2157 - getters傳回預設隱藏字幕樣式，即使在串流上設定並以視覺化方式驗證不同的樣式。 「隱藏字幕」樣式屬性現在會顯示已設定的值。

## 1.4 {#known-issues-in}中的已知問題

**1.4.31版**

* PTPLAY-16803 —— 隱藏字幕將不能處理僅音頻內容，因為字幕系統需要視頻才能工作。 沒有視訊，就沒有視訊檢視區尺寸，沒有視訊檢視區尺寸，我們就無法顯示標題的圖形。
* PTPLAY-1634 —— 相同訂閱標籤在不同即時視窗中有不同的時間戳記。 當即時視窗移動時，其中的相同標籤應具有相同的時間戳記。 但是，有時候，即使是相同的標籤也會有不同的時間戳記。
* PTPLAY-3197 —— 連續播放約1小時後，Acer Iconia裝置上發生信號11 SIGSEGV錯誤，當機
* PTPLAY-3310 —— 使用較低位元速率的音訊，Acer Iconia的音訊變得不順暢／不順暢
* PTPLAY-3355 —— 在持續播放約1小時後，使用4.0.x在Motorola Xoom上發生WIN DEATH當機。
* PTPLAY-3557 —— 在廣告中斷時倒帶導致串流完成
* PTPLAY-7079 - Android用戶端上的「播放視窗」無法與「保全停止／硬停止」搭配運作
* 錯誤#3760144 —— 在Kindle Fire 7和Samsung Galaxy Nexus等裝置上暫停串流時，解析度可能會偏移或看似脈衝。 僅可觀察
* 錯誤#3761170 —— 使用廣告即時搜尋的seekToLocal無法尋找廣告內容，它最適合使用即時串流的目前時間API
* 錯誤#3763370 —— 含廣告的即時串流偶爾會在應該只有一個廣告時，顯示兩個相近的廣告標籤。 這些廣告標籤代表相同的廣告，只會有一個
* 錯誤#3763373 —— 在VOD串流中透過廣告時，廣告標籤可能會短暫消失。 廣告標籤會還原，而且時間軸上沒有其他負面效果
* 有些裝置有已知的播放問題。 請參閱1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)中的[已知設備問題。
* 參考實作——範例應用程式中未實作特技播放
* 在某些Android TV裝置上，由於解碼器在下列轉場點重設，所以可看到黑色影格：
   * 進入和退齣戲劇模式
   * 切換延遲綁定音軌
   * 從廣告到主要內容。

**1.4.23版**

* 隱藏字幕無法處理純音訊內容，因為字幕系統需要視訊才能運作。 沒有視訊，就沒有視訊區尺寸，沒有視訊區尺寸，就無法顯示標題的任何圖形。
* 從1.4.23版開始，TVSDK將不支援Gingerbread OS 2.3。這是因為TVSDK使用下列私人Android程式庫來收集Gingerbread OS裝置的硬體資訊：

   * `libstagefright.so`
   * `libcutils.so`

在Android N版本中，Google已移除這些私用程式庫的存取權。 Gingerbread OS目前在全球Android OS市場佔有率不到1%，因此在1.4.23版之後，TVSDK將不再支援Gingerbread OS。
當您使用1.4.23版（包含Android N支援）或更新版本時：
* 更新您的應用程式以使用minSdk第11版。
* 如果您的使用者執行的是OS 2.3，則SDK版本會低於應用程式的minSdkVersion。 系統中止應用程式的安裝或升級。
* 如果您的使用者執行的版本高於OS 2.3，應用程式將會正確安裝。

如果您更新minSdk版本：

* 如果您的使用者執行OS 2.3，應用程式會安裝，但播放將無法運作。
這同時適用於更新和最新安裝。
* 如果您的使用者執行的系統高於OS 2.3，應用程式會正確安裝，而內容會正確播放。

**1.4.22版**

* 當剪接和剪接標籤彼此太接近時，早期退出廣告無法用於某些中端廣告。

**1.4.2版**

* 在廣告中斷時倒帶會導致串流完成。

Media Player會在Trick Play倒轉作業期間，將MediaPlayer PlayerState錯誤地傳送出來。當它到達廣告界限時，完成。 當播放器處於特技播放模式時，應忽略此事件，否則SDK會正確處理狀態。

**1.4.0版(1086)**

* PTPLAY-1634 —— 相同的「已訂閱」標籤在不同即時視窗中有不同的時間戳記。 當即時視窗移動時，每個視窗中的相同標籤都應有相同的時間戳記。 但是，有時候，即使是相同的標籤也會有不同的時間戳記。
* PTPLAY-2541 —— 在封鎖期中往／返備用流的數個交換機之後，有時會看到COMPONENT_CREATION_FAILURE
* 錯誤#3726865 —— 如果多位元速率LBA串流從僅音訊串流開始，則切換至音訊／視訊串流時，將不會顯示視訊。 從音訊／視訊串流開始將不會顯示此問題，而且可以在音訊和音訊／視訊串流之間成功切換
* 錯誤#3760144 —— 某些裝置（例如Kindle Fire 7和Samsung Galaxy Nexus）暫停串流時，解析度可能會偏移或看似脈衝。 僅可觀察
* 錯誤#3761170 - seekToLocal in Live with Ads無法重新搜尋廣告內容；最好使用目前即時串流的currentTime API
* 錯誤#3763370 —— 含廣告的即時串流偶爾會在應該只有一個廣告時，顯示兩個相近的廣告標籤。 這些廣告標籤代表相同的廣告，只會有一個
* 錯誤#3763373 —— 在VOD串流中透過廣告時，廣告標籤可能會短暫消失。 廣告標籤會還原，而且時間軸上沒有其他負面效果
* 有些裝置有已知的播放問題。 如需詳細資訊，請參閱1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)中的[已知裝置問題。
* 參考實作——特技播放未在範例應用程式中實作。

## 1.4 {#known-device-issues-in}中的已知設備問題

| 裝置 | 晶片集 | 問題 | 原因 | 解決方法 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR延遲是預期的，因為它正在重新啟動解碼器。 |  |  |
| HTC Desire（與HTC Desire HD不同） | QSD8250 | 無法播放視訊。 傳回VIDEO_PROFILE_NOT_SUPPORTED錯誤。 | 需要的HW解碼器不正確。 它提供Stagefright的軟體解碼器。 | 重新啟動設備。 |
| HTC EVO 4G | QSD8650 | 無硬體解碼器。 | Qualcomm沒有硬體解碼器。 | 升級至Android 4.x。 |
| Kindle FireSystem 6.0版 | TI OMAP4 | 不播放HLS串流。 AIR上的視訊無法運作。 |  | 升級至系統6.3版。 |
| Kindle Fire HD | TI OMAP4 | 可進入無法播放視訊的狀態。 傳回VIDEO_PROFILE_NOT_SUPPORTED和UNRECOVABLE_ERROR錯誤。 | 當應用程式未完全關閉HW解碼器時（例如，在遇到當機後）,HW解碼器會進入不可恢復狀態。 裝置上的原生應用程式也會發生。 | 重新啟動設備。 |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE在多個ABR交換機後崩潰。 |  |  |
| Motorola Atrix | 特格拉2 | 相較於AIR,AVE的整體效能問題。 音訊／視訊失去同步，視訊播放在播放9到15分鐘後就會停止。 當機。 | 可能與我們在AIR上啟用的openGLES有關。 正在接受調查。 |  |
| Nexus 7（第2代） | S4Pro APQ8064(Qualcomm) | 當影片暫停超過30分鐘時，裝置會掛起。 | 已回報給Google的裝置問題。 | 應用程式應逾時，以免出現長暫停狀態。 |
| Nexus S(GB) | 嗡嗡鳥 | 無法使用HW解碼器播放任何視訊。 | Nexus S中沒有採用Stagefright的硬體解碼器，因此，我們針對Android 2.3使用軟體解碼器。 | 升級至ICS。 |
| Nexus S(ICS) | 嗡嗡鳥 | 視訊偶爾會閃爍。 | 不良資料會導致解碼器進入不良狀態。 | 重新啟動設備。 |
| Nook tabletAndroid OS:2.3 | TI OMAP 4 | 視訊無法播放，而應用程式也暫停。 | Stagefright在執行應用程式幾次後進入不穩定狀態。 呼叫mediaplayer::QueryCodecs暫停。 | 重新啟動設備以重置狀態。 |
| Samsung Galaxy ACE | Qualcomm MSM7227 | 無法安裝SampleMediaPlayer應用程式。 | 使用ARM v6而非更常見的ARM v7晶片集。 FP/AIR不支援此裝置。 |  |
| Samsung Galaxy ACE2Android作業系統：2.3.6 | NovaThor U8500 | 無法播放視訊。 | 此晶片集是AVE中Android pre-ICS的未知解碼器。 |  |
| Samsung Galaxy S2(GT-I9100) | Exynos | 視訊效能不及此裝置的等級。 | HW解碼器返回具有錯誤PTS的解碼幀。 看來解碼器使用的是解碼時間而非呈現時間。 |  |
| Samsung Galaxy S2 GAndroid OS:2.3.6 | TI OMAP4 | 啟動視訊時當機。 |  | 升級至Android 2.3.7或4.x。 |
| Samsung Galaxy S3(I747) | Qualcomm MSM8960 | 視訊偶爾會凍結，只播放音訊，然後停止回應。 |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | 視訊凍結。 | 調查。 |  |
| Samsung Galaxy Tab 1 v10.1 | 特格拉2 | MBR轉換最多需要3秒。 | 當MBR當機時，我們會重新啟動每個串流交換機的解碼器，最多需要三秒。 |  |
| Samsung Galaxy Y |  | 無法安裝SampleMediaPlayer應用程式。 | 使用ARM v6而非更常見的ARM v7晶片集。 FP/AIR不支援此裝置。 |  |
| Xoom | 特格拉 | 會捨棄一些幀以進行切換。 解碼器未重新啟動。 | OMXAL限制。 |  |

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。
