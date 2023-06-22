---
title: Android適用的TVSDK 1.4發行說明
description: Android適用的TVSDK 1.4發行說明說明TVSDK Android 1.4的新增或變更專案、已解決和已知問題以及裝置問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 1e3ec3b7-25be-4640-870e-928e832fe12d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# Android適用的TVSDK 1.4發行說明 {#tvsdk-for-android-release-notes}

Android適用的TVSDK 1.4發行說明說明TVSDK Android 1.4的新增或變更專案、已解決和已知問題以及裝置問題。

## 新功能 {#new-features}

**版本1.4.43**

**安全透過HTTPS載入廣告**

Adobe Primetime提供可透過HTTPS要求第一次呼叫primetime廣告伺服器和CRS的選項。

**MediaPlayer類別中的alwaysUseAudioOutputLatency（布林值）**

設定此引數時，請在音訊時間戳記計算中使用音訊輸出延遲。

它接受布林值引數val。 若其值為 `True`，使用者端會在音訊時間戳記計算中使用音訊輸出延遲。

**版本1.4.42**

**部分廣告插播插入：**
在廣告中間加入，而不引發部分觀看廣告追蹤的電視體驗。
範例：使用者在包含三個30秒廣告的90秒廣告插播中間（在40秒）加入。 這是插播中第二個廣告的10秒。
* 第二個廣告會播放剩餘的持續時間（20秒），接著是第三個廣告。
* 部分已播放廣告（第二個廣告）的廣告追蹤器未觸發。 只會觸發第三個廣告的追蹤器。

**版本1.4.41**

沒有新功能。

**1.4.40版**

沒有新功能。

>[!NOTE]
>
>如果您使用1.4.39之前的版本，則不需要變更API。

**版本1.4.39**

* TVSDK已通過VHL 2.0.1和VHL 2.0.1的認證，並與Nielsen合作。
* Android TVSDK已更新，可從新的Akamai主機發出CRS請求 `primetime-a.akamaihd.net`.
* 新的主機名稱設定可大幅透過HTTP和HTTPS (SSL)提供CRS資產傳遞。
* TVSDK支援Android Oreo版本。
* 新函式已新增至 `AdClientFactory` 類別以支援註冊多個機會偵測器：

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   這應該會傳回PlacementOpportunityDetector陣列。 現在您可以註冊多個機會偵測器。 例如，對於早期廣告退出功能，需要兩個機會偵測器 — 一個用於廣告插入，另一個用於早期退出廣告。 只有在您已實作自己的AdvertisingFactory （且不使用DefaultAdvertisingfactory）時，才需要實作此新功能。 若要取得現有行為，您需要建立單一機會偵測器，如createOpportunityDetector()函式，並放入陣列中傳回：

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
>如果您使用1.4.39之前的版本，則不需要變更API。

**版本1.4.36**

Android上內容略過的錯誤修正。

**版本1.4.35**

* **網路廣告資訊**

   TVSDK API現在提供有關第三方VAST回應的其他資訊。 廣告ID、廣告系統和VAST廣告擴充功能會提供在NetworkAdInfo類別中，可透過廣告資產上的networkAdInfo屬性存取。 此資訊可用於與其他Ad Analytics平台整合，例如 **Moat Analytics**.

**版本1.4.31**

**CRS Ads的多重CDN支援**
* 依預設，所有轉碼資產都會在Akamai上Adobe擁有的CDN上託管。 在最新版本中，Adobe Creative Repackaging Service (CRS)可讓您將轉碼創意內容上傳至客戶指定的多個CDN。
* 新API會新增至TVSDK，以便在不使用預設url時指定最終CRS創意url。 請參閱檔案以瞭解如何使用這些新API。

**版本1.4.18**
Primetime Android TVSDK現在支援VPAID 2.0 Javascript創意，以提供豐富的互動式串流廣告體驗。 如需VPAID 2.0的詳細資訊，請參閱 [VPAID廣告支援](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**版本1.4.17**

只有Amazon FireTV支援AC-3 5.1。

**版本1.4.11**

* **廣告遞補、廣告選擇邏輯中的Daisy鏈結(Zendesk #3103** 對於已啟用遞補規則的VAST廣告（創意內容），TVSDK會將具有無效MIME型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

如需詳細資訊，請參閱 [VAST和VMAP廣告的廣告遞補](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **視訊心率程式庫(VHL)更新至1.5版**
   * 能夠連同視訊開始和/或視訊/廣告/章節開始一起傳送中繼資料作為內容資料
   * 網路流量較少 — 心率平均而言更少，且大小較小

**版本1.4.7**

* **內部部署個人化支援**&#x200B;支援Adobe個人化伺服器的內部部署安裝，可自訂使用者端的個人化請求，以移至其他端點。

**版本1.4.6**

* **範例AES加密(需要Flash Player版本17.0.0.134)**現在支援範例型AES加密。

**版本1.4.2**

* **視訊心率程式庫(VHL)更新至1.4.0.1版**

   * 新增將其他SDK或播放器中的不同Analytics使用案例與Adobe Analytics Video Essentials搭配的功能。
   * 已透過移除trackAdBreakStart和trackAdBreakComplete方法最佳化廣告追蹤。 廣告插播是從trackAdStart和trackAdComplete方法呼叫中推斷出來的。
   * 追蹤廣告時不再需要播放點屬性。

* **Nielsen SDK整合** TVSDK現在支援將使用者追蹤資訊傳送至Nielsen SDK，無需任何自訂整合。

**1.4.0版**

* **使用替代內容取代發出中斷訊號** 在1.4 TVSDK更新中，TVSDK現在也支援進入及從線性內容的區域中斷返回。 TVSDK現在可以並行處理兩個資訊清單檔案（主要和替代），以監控中斷訊號，即使替代程式設計正在取代原始程式設計。

* **移除/取代C3廣告** 現在，不需要額外的準備工作，即可動態地將新廣告插入從C3視窗傳出的隨選影片(VOD)資產。 TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 在廣播期間播放即時/線性內容，並立即下拉以供隨選內容使用（沒有適當的時間來「清除」資產）的情況下，這項強大的新功能也很有用。

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，您可以使用它來接聽新事件。 `ITEM_REPLACED`. 每當在MediaPlayer上取代MediaPlayeritem例項時，就會傳送此事件。 實作此PlaybackEventListener的使用者端應用程式必須實作或覆寫這個新方法。
* AdClientFactory在類別中新增了一個新函式，以註冊多個機會偵測器：

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

## 1.4的TVSDK變更 {#tvsdk-changes}

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，可用來接聽新事件ITEM_REPLACED。 每當在MediaPlayer上取代MediaPlayeritem例項時，就會傳送此事件。 實作此PlaybackEventListener的使用者端應用程式必須實作或覆寫這個新方法。

* AdClientFactory在類別中新增了一個新函式，以註冊多個機會偵測器：

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

例如，若是廣告提前退出功能，您需要兩個機會偵測器 — 一個用於廣告插入，另一個用於廣告提前退出。

若要覆寫此新函式，請建立單一Opportunity Detector，然後放入陣列並傳回：

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4版的裝置認證與支援 {#device-certification-and-support-in}

>[!NOTE]
>
>下列功能為 **not** TVSDK支援：
>
>* 在任何平台或版本上，動作緩慢。
>* 即時特技播放。


**版本1.4.43**

TVSDK 1.4.43已通過Android裝置認證，具有Android 6.0.1/ 7.0和8.1 (Oreo)。

* **1.4.23版：**

   * TVSDK 1.4.23已針對採用Android N的Android裝置通過認證。

* **1.4.18版：**

   * Primetime已通過Amazon Fire TV的認證。
   * VPAID 2.0僅支援搭配Android 4.0及更高版本的裝置。

## 1.4中已解決的問題 {#resolved-issues-in}

>[!NOTE]
>
>強烈建議所有使用CRS的TVSDK客戶升級至iOS和Android上的TVSDK 1.4.39版或最新版本。 此升級是現有應用程式實作的下拉式替代程式。 升級後，請在Proxy工具（例如Charles）中檢查CRS創意URL請求，以驗證路徑中的版本是否反映3.1版。例如：
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**版本1.4.43**

* 票證#27143 — 無法在FireTV裝置上播放5.1音軌

   * TVSDK現在可以在FireTV裝置上播放AC3音訊。 播放一律為立體聲。

* 票證#33902 — 透過HTTPS的安全廣告傳送

   * Adobe Primetime提供可透過https要求第一次呼叫primetime廣告伺服器和CRS的選項。

* 票證#34493 — 藍芽音訊延遲

   * 已新增 `alwaysUseAudioOutputLatency` 在MediaPlayer類別中，設定此值時，將導致在音訊時間戳記計算中使用音訊輸出延遲。

* 票證#34949 — 整合了新版本的視訊心率程式庫(VHL)。

**1.4.42版(1791)**

* Zendesk #33719：FireTV 4k最適化位元速率縮放緩慢。 新增FireTV 4K裝置的ABR支援。
* Zendesk #33338： resetDRM會清除應用程式的所有資料。  處理非TVSDK執行緒中的例外狀況導致TVSDK操作佇列填滿的額外情況。

**1.4.41版(1776)**

* Zendesk #33002 - Fire TV上TVSDK的隨附資產資料。 實作新類別AdBannerAsset，此類別會將Companion資料傳回為List &lt;adbannerasset> 和AdAsset：：id現在是字串而不是長字串。
* Zendesk #32821 — 遇到WWE的簡報時間戳記(PTS)時，Android Primetime播放器會凍結。 此問題已在此版本中修正。
* Zendesk #33572 - VideoAnalyticsProvider廣告開始當機。 使用VideoHeartbeat.jar的VHL+Nielsen聯合SDK版本的正確組合已修正此問題。
* Zendesk #33355 - Fire TV：擦除15秒問題。 沒有任何來自TVSDK端的修正，且客戶正在其終端和第三方驗證此修正。

**1.4.40版(1764)**

* Zendesk #33068 — 新裝置上的Amazon lip sync問題。 此版本已修正唇語同步問題。
* Zendesk #32215 - Android TVSDK 1.4.38安全性問題 `[Hotlist]`. 更新至最新的OpenSSL-1.1.0和curl-7.55.1。
* Zendesk #32920 — 廣告插播內的空白畫面且沒有廣告插播完成。 修正VPAID容器可能進入擱置狀態的問題，並處理Facebook VPAID廣告通常在單一\&amp;lt；AdParameters\&amp;gt； VAST節點中傳回多個CDATA區塊的問題。

**1.4.39版(1744)**

* Zendesk #28976 — 授權請求需要超過一秒鐘的時間。 使用POST的DRM授權要求呼叫在執行時，Curl會新增額外的「Expect： 100-continue」標頭。 移除TVSDK中的「Expect：」標頭。
* Zendesk #27707 - CSAI環境不接受CUE IN標籤以提早返回或返回內容。 為多個機會產生器提供支援。

**1.4.38版(1722)**

* Zendesk #21590 — 最新來源組建中的視訊效能和追蹤

整合及認證TVSDK中的VHL 2.0，降低API的複雜性，進而降低VideoHeartbeatsLibrary實作中的障礙。

* Zendesk #29688 - Android O測試版客戶支援。

新Android測試版的TVSDK支援。

**1.4.36版(1713)**

* Zendesk #27392 - Android上的內容略過

為了配合解密，Android TVSDK錯誤地將non-iframe內容的位元組範圍擴大了16個位元組。 Iframe資料流需要加寬，但非iframe資料流則不需要。

**1.4.34版(1702)**

* Zendesk #27638 - cURL INet物件中洩漏

Posix cURL INet物件在保留在cURL連線中使用的共用管理員和DNS快取時遺漏。

此問題已透過從INet解構函式刪除Posix cURL INet物件來解決。

**1.4.33版(1694)**

* **OpenSSL程式庫**

OpenSSL程式庫已更新為OpenSSL 1.0.2j版。

* Zendesk #21701 — 傳送1401 CRS請求的原始創意URL，而不是標準化的URL。
此問題可透過傳送原始創作URL來解決。

* Zendesk #25023 — 長期間視訊播放：視訊凍結、熒幕閃爍此問題已透過設定CenturyLink機上盒裝置的視訊格式尺寸上限來解決。

* Zendesk #27460 — 新的Akamai帳戶無法處理POSTcdn請求。
程式碼已更新，以使 `cdn.auditude.com` 廣告要求是GET而非POST。

* Zendesk #28245 — 應用程式從背景移至前景時，播放狀態未正確通知。當應用程式返回前景時，可正確將播放狀態還原為播放或暫停，以解決此問題。

**1.4.32版(1682)**

* Zendesk #25779 — 在WebView中啟用JavaScript時，TVSDK Android 4.2及以下版本出現安全性弱點。 執行OS 4.2或更低版本的裝置已停用透過TVSDK使用WebView。 如此一來，在這些裝置上將無法在TVSDK中使用VPAID廣告。

* Zendesk #26890 — 熒幕狀態（開啟/關閉）中的問題處理參考 播放器Adobe視訊引擎(AVE)從「已擱置」狀態恢復時，DefaultMediaPlayer不會更新其狀態。 因此，即使AVE處於PLAYING狀態，DefaultMediaPlayer仍會維持在SUSPENDED狀態。 當從AVE收到PLAY狀態時，將DefaultMediaPlayer狀態設定為PLAYING，即使DefaultMediaPlayer目前的狀態為SUSPENDED，此問題已解決。

**1.4.31版(1675)**

* Zendesk #21974 — 由於Null物件產生的例外
   * AdIndex很少在為null時增加。 這可能是因為前段廣告插播收到的API呼叫不正確。 修正資料型別以避免此類例外

* Zendesk #24714 — 關閉無關的記錄
   * 更新TVSDK以關閉無關記錄

* Zendesk #24488 - Fire TV上的AV同步問題
   * 已藉由改善處理AV解碼器執行緒的方式加以修正。 具體而言，每當修改輸入或輸出框架佇列時，就會執行框架內容型別特定的解碼器執行緒。

* Zendesk #26551 — 修正CRS故障
   * 當請求HEAD(http head)時，我們不需要讀取內容，因為它是空的。 雖然可以嘗試讀取，但我們呼叫read()時會掛斷舊版Android (4.0.x)，而呼叫read()時較新版Android會傳回正確的值(-1)。 根據此，將程式碼變更為不讀取「head」的內容

* 存取TrickPlayManager時Zendesk#26696Null指標例外狀況
   * 使用前先檢查TrickPlayManager物件是否為Null即可修正。

**1.4.30版(1659)**

* 沒有針對即時/線性資料流更新Zendesk #22675資產持續時間此問題已解決，方法是在PTVideoAnalyticsTrackingMetadata中提供新的API assetDuration，提供即時和線性資料流的資產持續時間。

* Zendesk #25853切換頻道時TVSDK中的記憶體洩漏已解決在下載檔案時重設或釋放MediaPlayer時的檔案讀取緩衝區洩漏問題。

**1.4.29版(1653)**

* Zendesk #21200 — 當應用程式於背景時，播放器不會從暫停狀態復原當播放器在收到串流切換的訊號後暫停時，此解決方法可讓播放器在播放器從暫停狀態回覆時執行串流切換，而不是回復到先前的位置。

* Zendesk #23412 — 如果您在廣告插播的最後3秒內點進任何廣告，播放器會卡在黑匣子中。此問題與Zendesk #21200的問題相同。

* Zendesk #23616 — 已略過的廣告插播在未來會搜尋太遠根據廣告插入型別（插入/取代），TVSDK會判斷計算中是否使用廣告持續時間來判斷廣告插播結束點。

* Zendesk #25078 - Android TV STB上的TVSDK DRM記憶體洩漏已找到並修正DRM介面卡物件的記憶體洩漏。

* Zendesk #25067 - VideoEngineTimeline中的當機發生此狀況是因為物件未正確清除，且在物件毀損後呼叫了事件。 透過新增檢查以防止Null例外狀況，此問題已解決。

* Zendesk #25352 — 設定自訂HTTP標頭此問題已透過在TVSDK上新增自訂標頭至允許清單而解決。

* Zendesk #25617 — 即時資料流PTS滑鼠指向效果造成播放器中斷和記憶體當機當滑鼠指向效果發生在區段中央時，在FragmentedHTTPStreamer中新增PTS滑鼠指向效果處理即可解決此問題。

**1.4.28版(1637)**

* Zendesk #23618 — 在諮詢廣告原則之前觸發廣告插播事件。此問題已解決，當廣告因adForgiveness而被略過時，未觸發AD_BREAK_START和AD_START事件。 而是傳送AD_BREAK_SKIPPED事件。

**1.4.27版(1631)**

* Zendesk #23174 — 重新調整視訊大小時的效能問題此問題已透過證明新API MediaPlayerView.setSurfaceFixedSize解決，此新API允許TVSDK從MediaPlayerView存取SurfaceHolder.setFixedSize()。

* Zendesk #24450 - TVSDK提出重複的廣告請求當經過的時間轉換為長而不是倍時，就會發生此問題，而且此問題已修正。

**1.4.26版(1627)**

* Zendesk #21436 - OpenSSL程式庫更新至1.0.2h版OpenSSL程式庫更新至1.0.2h版
* Zendesk #23825 — 回撥中不包含Cookie。藉由提供android Cookie支援加以修正。

**1.4.25版(1620)**

* Zendesk #22900 — 即時Adobe Primetime DRM資料流未在Android參考播放器上播放記憶體配置問題已解決。
* Zendesk #23176 — 應用程式嘗試播放VPAID廣告時當機當機因為應用程式未建立自訂廣告檢視來轉譯VPAID廣告而發生。 當沒有自訂廣告檢視時，此問題可透過忽略廣告伺服器回應中的VPAID廣告來解決。

* Zendesk #23153 - SampleAES DRM資料流 — TVSDK參考播放器中的播放延遲此問題與Zendesk #22900相同。

**1.4.24版(1612)**

* Zendesk #20784 - Analytics：觸發即時視訊轉換的內容完成此問題已藉由新增API (trackVideoComplete)解決，以便在即時/線性視訊追蹤工作階段期間手動觸發內容完成。

* placeAdBreak/acceptAd作業期間的Zendesk#21977VideoEngineTimeline當機
   * 在本期中，已更新下列程式庫：
      * AdobeMobile程式庫至4.10.0版
      * VHL程式庫至1.5.6版
      * VHL-Nielsen程式庫至1.6.7版

將廣告新增至接受的廣告清單之前，先新增Null檢查即可解決此問題。

* Zendesk #22313使用Amilogic晶片組之STB的位元速率不會超過1.2M此問題已透過預先載入媒體轉碼器功能並停用Amilogic晶片組裝置的無縫交換器來解決。

* Zendesk #19520在TVSDK播放器中不播放範例AES HLS資產此問題已透過處理範例AES加密HLS資料流的多個PMT描述項來解決。

**1.4.23版(1602)**

* Zendesk #18852 — 根據CRS規則更新創意選擇邏輯此問題已透過新增JSON設定檔案以指定創意選擇優先順序來解決。

* Zendesk #20861 - Android N此版本移除了直接使用Android平台原生程式庫（在Android N上執行的應用程式無法再存取這些程式庫）的功能，以支援Android N。

* Zendesk #21018 - Android N當機解析度與ZD# 20861相同。

* Zendesk #21266 - VideoEngineAdapter因Invalid_Key錯誤而當機Invalid_Key錯誤未包含來自AVE的說明，因此剖析文字會導致NPE。 在onError期間在剖析說明之前新增說明的null檢查，即可解決此問題。

* Zendesk #22286 — 原生程式庫正在配置記憶體讀取索引鍵/片段，導致當嘗試同時載入包含多個索引鍵的資訊清單時，Android上發生的此當機已修正。

**1.4.22版(1581)**

* Zendesk #17236 — 使用DRM的HLS視訊的播放點時間不可靠LBA串流的時間跳躍已修正，其中音訊區段開始時間與視訊區段開始時間不符。

* Zendesk #17680 — 在Selevision Andredo方塊上的視訊播放凍結。從輸出緩衝區將視訊影格取消佇列時，此裝置上的視訊解碼器有時會傳回顯著的輸出時間跳躍，而且此輸出時間戳記會維持在較高水準。 此問題已透過傳回 *不支援視訊設定檔* 不會強製播放器重試相同設定檔或選擇不同設定檔的錯誤。

* Zendesk #19074 - FFWD和REW特技播放期間視訊凍結此問題已解決，方法是新增警告TRICKPLAY_ENDED_DUE_TO_ERROR來通知應用程式trickplay已結束，且視訊已因無法復原的錯誤而暫停。

* Zendesk #19574 - TVSDK未傳回DRM或非DRM內容的M3U8回應資料此問題已透過下列方式解決：

* Zendesk #19986 — 某些裝置（例如Android TV）的OP行為已中斷
* 將FILE_NOT_FOUND錯誤新增至條件。
* 當錯誤來自 *找不到檔案* 錯誤，如果回應可用，則從錯誤說明中分隔URL和回應。
NVidia shield OP支援引入的邏輯錯誤已修正。 在非NVidia shield裝置上，即使顯示型別不明，也信任顯示安全旗標。

* Zendesk #20549 — 處理過時播放清單。 如果先前的擷取沒有收到新區段，此問題可透過將即時資訊清單更新之間的間隔縮短至預期區段期間的一半來解決。

* Zendesk #20742 — 在FireTV上播放即時內容時，記憶體使用量似乎持續增加。當機是由已達到限制的JNI物件參考表格所造成。 此問題已透過刪除在解碼器重新啟動期間建立的MediaFormat物件參考來解決。

* Zendesk #21125 — 從即時/線性廣告插播提早返回(CSAI)。 新增一項功能，如果播放器使用機會偵測器中的接合在廣告提示中註冊接合，可讓播放器在廣告插播期間返回主要內容。

* Zendesk #21334 — 第三方廣告請求的TVSDK廣告請求逾時值。 已將adRequestTimeout設定新增至AdvertisingMetadata，可為廣告呼叫啟用全域逾時。

**1.4.21版(1566)**

* Zendesk #17781 - ADB熒幕擷取不再運作此問題已透過新增允許熒幕擷取的DefaultMediaPlayer.create(Context context，boolean secureSurface) API解決。
若要允許熒幕擷取，請為secureSurface傳遞false。
重要：強烈建議您不要在生產設定中啟用此熒幕擷取功能。

* Zendesk #19074 — 在FFWD和REW特技播放期間視訊凍結特技播放中可能發生的特技播放凍結的下列問題已解決：

* Zendesk #19532 — 隱藏式字幕顯示順序錯誤
   * FHS會開始逐步播放，但第一個iframe區段沒有框架。
   * 下載iframe區段時，如果FHS點選錯誤條件，則會從Trickplay結束，並暫停播放。
   * Andorid MediaCodec實作會在要求排清所有輸入/輸出緩衝區時，永遠等待輸入佇列可用性。
此問題已透過反轉WebVTT提示的順序來解決，使得多個重疊提示看起來像是「向上捲動」。

* Zendesk #19574 - TVSDK不會傳回DRM或非DRM內容的M3U8回應資料。在PTMediaPlayerItem.prepareToPlay中的資訊清單檔案的初始載入中，如果載入失敗，TVSDK不會向應用程式報告失敗回應的內文。
允許TVSDK將失敗回應回報給應用程式，即可解決此問題。

* Zendesk #19701 — 播放因SAP/中斷而凍結當音訊和視訊中斷而解除對齊時，播放器會凍結，問題已解決。

* 錯誤#PTPLAY-11162 — 已解決OpenSSL程式庫更新至1.0.2f版的問題。

**1.4.20版(1546)**

* Zendesk #17384 — 功能要求： 1.4.20版以後的Android TVSDK已提供AAC媒體中ID3標籤的AAC播放支援。

* Zendesk #18358 — 位元速率交換器上播放器凍結，且中斷不同步。此問題可透過適當處理ABR彙整邊緣案例來解決。

* Zendesk #19232 — 使用TVSDK 1.4.18的應用程式在舊版Amazon作業系統4上的行為異常此問題已解決，方法是移除在TVSDK播放器初始化程式中建立的隱藏Web檢視，以避免與不支援Android Webview的裝置衝突。

* Zendesk #19585 — 發生最適化位元速率轉換時的慢動作播放。
在ABR切換期間，如果新設定檔的音訊取樣速率與目前設定檔不同，則播放會變成快速或慢動作。 這是因為未通知視訊簡報者音訊格式已變更。
此問題已透過確定通知旗標已設定在正確位置而解決。

* Zendesk #19683 - SAP DAI播放 — 數秒無音訊。
在TVSDK邏輯中的數個案例中，當比較兩個轉譯區段的時間戳記時，會使用RENDITION_TIMEOUT_THRESHOLD作為可接受的值範圍，因為時間戳記無法一律符合0毫秒的差異。 如果間隙在RENDITION_TIMEOUT_THRESHOLD範圍內，則假設它是相符的。

RENDITION_TIMEOUT_THRESHOLD設定為100毫秒，但發現某些資料流不足。 將RENDITION_TIMEOUT_THRESHOLD增加到200毫秒，即可解決此問題。

* Zendesk #19699 - TVSDK無法在VTT字幕曲目之間切換此問題已解決，方法是在曲目變更時進行播放器傾印並重新載入資訊清單，以及修正影響雙位元WebVTT插圖示題曲目名稱的UTF8字串轉換問題。

* Zendesk #19717 - CC選項顯示問題此問題已透過正確處理Unicode字串而解決。

* Zendesk #19910 — 未偵測到TIT2 ID3標籤此問題已解決，方法是為ID3 v2.4字串編碼和ID3 v2.3支援提供更完整的支援。

* Zendesk #20135 - TVSDK正在觸發VOD內容的多個onComplete。
此問題已透過在正確位置新增post_roll_complete事件接聽程式而解決，而不是在狀態變更事件的完整情況下解決。

**1.4.19版(1521)**

* Zendesk #4180 - TVSDK未強制執行HDCP。
   * 此為本票證的部分修正，僅解決NVidia盾牌裝置的問題。
您必須在Nvidia Shield中使用正確實作的HDCP偵測API，才能動態追蹤HDCP狀態。

* Zendesk #18358 - TVSDK會在位元速率交換器上凍結，且會失去同步的不連續性。
   * 此問題已透過新增警告來偵測PTS不連續性，並強制PTS檢查重做搜尋每個ABR交換器的正確區段來解決。
若要修正凍結，對mediaPlayer.setCustomConfiguration方法的呼叫應包含forcePTSCheckForABR作為引數。

* Zendesk #19038 - Asus Zenpad 10上無即時資料流。

   此問題已透過預先載入媒體轉碼器資訊來解決，因此您不會在執行階段查詢函式。

* 以下問題與Zendesk #19038相同：
   * Zendesk #19483 - TVSDK在Intel平台上當機。
   * Zendesk #19171 — 使用Android 5.0在Asus Memo Pad 7上當機。

**1.4.18版(1503)**

* Zendesk #3324 - VMAP中沒有廣告媒體時，Primetime廣告報告不會追蹤廣告插播。
當廣告插播為空白時，系統未偵測到廣告插播開始和完成追蹤事件。 此問題已透過在空白廣告插播（例如VMAP AdBreak）上使用有效的AdSource節點傳送廣告插播開始Ping來解決。

* Zendesk #18229 - SetCCVisiblity(VISIBLE)在MediaPlayer.reset()呼叫後遭到忽略。此問題已透過將setCCVisibility（Visibility.不可見）；新增至MedIAPlAYER類別中的RESET()函式而解決。

* Zendesk #18328 - Amazon Fire TV第2代裝置上使用60FPS內容的掉格問題此問題已透過套用編碼FPS用於睡眠時間決策，並使用更好的編碼FPS預測邏輯來解決。

**1.4.17版(1472)**

* Zendesk #2231 — 擷取MediaPlayerNotification中無法使用的資訊清單傳回的錯誤。此問題已透過在出現剖析錯誤時包含資訊清單的回應本文來解決。

* Zendesk #17703 - VideoEngineView不會防止在視訊播放期間擷取熒幕畫面setSecure方法自API 17起便已推出，但由於API 17涵蓋4.2、4.2.1和4.2.2，因此不清楚哪一個會擲回例外狀況，或是否為裝置所特有。 將VideoEngineView.setSecure包裝到try catch子句中即可解決此問題。

* Zendesk #17919 — 內容搜尋導致心率錯誤無效輸入資料位置錯誤是由於在前置播放後開始搜尋時產生的心率呼叫所造成。 此問題已解決。

**1.4.16安培** (1454a)

* Zendesk #18215 — 某些AES資料流無法載入。
在載入AES金鑰之前，先檢查設定檔DRM中繼資料大小，即可解決此問題。

**1.4.16版(1454)**

* Zendesk #3875 — 播放期間索引標籤S當機回覆CRS對Auditude的OKHTTP相依性，因為TVSDK現在直接使用httpurlconnection而非curl。 此問題已透過在發出任何其他JNI呼叫之前清除例外來解決。

* Zendesk #4487 — 追蹤內容的線性頻道線上性資料流播放工作階段期間，允許重新初始化視訊心率追蹤器，以解決此問題。

* Zendesk #17919 - Android — 內容搜尋導致心率錯誤當章節中有搜尋時，心率處於錯誤狀態的問題已解決。

* Zendesk #18053 - Adobe Primetime在棉花糖上當機TVSDK在Android M作業系統上當機，當時TVSDK程式庫使用會進行YUV ->RGB色彩轉換的霓虹燈。 透過使用非霓虹色版本的程式碼更新導致此問題的函式，此問題已得到解決。

* Zendesk #18072 - Android M — 應用程式當檢查是否支援設定檔和層級時，呼叫MediaCodecList和MediaCodecInfo API時會發生當機。 此問題已透過提前載入所有轉碼器資訊以提供暫時解決方法解決，以避免僅在需要轉碼器資訊時呼叫這些API。

* Zendesk #18074 — 使用Android 6.0時Nexus無法使用的阿拉伯字幕。透過為Android提供CTS字型地圖支援，該問題得以解決。

**1.4.15版更新(1438)**

* Zendesk #17437 — 使用某些AES資料流啟動VOD內容時的長時間延遲。
若要解決此問題，如果資訊清單中列出多個金鑰，請同時下載所有AES金鑰。

**1.4.15版(1435)**

* Zendesk #4278 — 最適化位元速率變更(ABR)時Android機上盒發生問題。
此修正的目的是使用最新的Android媒體轉碼器新增支援無縫ABR切換。

* Zendesk #17063 — 呼叫mediaPlayer.reset()會導致視訊引擎重設錯誤。
此修正是在傳送ErrorEvents時包含來自VideoEngineExceptions的原始MediaErrorCode。

* Zendesk #17130 — 在FireTV上看到變更位元速率時，短暫但明顯的暫停。
(與上述#4278相同)修正的目的是使用最新的Android媒體轉碼器，新增對無縫ABR交換器的支援。

* Zendesk #17666 — 其他廣告標籤，恢復內容時未預期或沒有廣告。
修正針對隨選視訊(VOD)內容執行prepareToPlay時，初始搜尋會在當地時間執行，而非虛擬時間執行的問題。

* Zendesk #17437 — 使用某些AES資料流啟動VOD內容時的長時間延遲。
此修正是當資訊清單中列出多個金鑰時，同時下載所有AES金鑰。

* Zendesk #17851 - Android TV - ABR期間的黑色影格。修正的目的是指定KEY_MAX_WIDTH和KEY_MAX_HEIGHT以啟用最適化播放。

**1.4.14版(1415)**

* Zendesk #3875 — 播放期間索引標籤S當機。
需要進行額外的修正以防止當機。

* Zendesk #17245 - Android TV的遞補功能無法運作。
修正啟用遞補功能時，播放擱置以及VMAP回應有空白廣告插播的其他問題。

**1.4.14版(1412)**

* Zendesk #17245 - Android TV的遞補功能無法運作。
移除對後援廣告停用創意重新封裝的限制。

**1.4.13版(1388)**

* Zendesk #3502 — 廣告插播期間的HLS使用者端容錯移轉支援允許在更新即時設定檔錯誤時容錯移轉至主要資訊清單。

* Zendesk #3875 — 播放期間索引標籤S當機若要解決HttpUrlConnection和cURLm之間的衝突，請使用協力廠商程式庫。

* Zendesk #4450 — 為內容解析器中的單一版位設定自訂中繼資料的問題將設定器新增到Opportunity設定。

**1.4.12版(1388)**

* Zendesk #2751 - CSAI和CRS |增強：處理特定媒體檔案URL中的動態元素。
更新Creative重新封裝服務，以正確處理具有動態創意URL的廣告。

* Zendesk #3965 — 從點按播放切換回正常播放，導致在開始播放之前向前跳躍一點。
   * Fix包含TVSDK，它會傳回速率變更之前的時間，直到所有變數都更新為止，而不是嘗試計算GetStreamTime。
   * 修正在接近資料流結尾處變更特技播放速度時的當機問題。
   * 修正特技播放期間目前的時間計算。

* Zendesk #3978 — 在8倍和16倍速玩耍時經常凍結。
   * 請一律選擇具有最低位元速率的技巧播放設定檔，以避免持續緩衝。
   * 增加略過影格間隔以獲得高特技播放率。
   * 修正在Trick Play期間達到目標長度後，緩衝區繼續增加的問題。

* Zendesk#3992援 — 額外的Trickplay速度
TrickPlay已更新為接受高於16x的速率；+/- 32、+/-64和+/-128現在也允許使用。

* Zendesk #4007 — 將GEOB物件解譯為時間軸中繼資料（Android和Web）的一部分。
新增setByteArray和getByteArray API。

* PTPLAY-7301 — 在隨機存取點立即啟動。
即時開啟已更新為允許非零起點。

**1.4.11版(1363)**

* Zendesk #2076 — 使用Android 4.0.3在Motorola Xoom上播放視訊時經常出現結巴。新增裝置以允許清單，以防止它們嘗試播放高設定檔內容。

* Zendesk #2197 - `[Ads]` 追蹤和錯誤傳送帶有警告通知的OperationFailedEvent。

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填入巨集
   * 如果內嵌廣告具有不良創意，則會顯示錯誤代碼400。
   * `[ERRORCODE]` 巨集將會進行URL編碼

**1.4.10版(1354)**

* Zendesk #2941 — 即時資產在可搜尋的範圍中沒有「0」之前在搜尋即時資料流的開頭時有3個區段緩衝區，現在可以搜尋即時資料流的開頭了（亦即第一個區段的開頭）。

* Zendesk #3169 — 透過Adobe Analytics整合更新參考播放器參考播放器已更新，Adobe Analytics程式庫為植入範例。
* Zendesk #3299 — 無法解釋的戲法玩耍行為
   * 修正停止特技播放後返回播放狀態可能需要幾秒鐘（有時超過25秒）的錯誤。
   * 修正在相同媒體上再次叫用特技播放可能會導致目前資料流凍結的錯誤。
* Zendesk #3433 - Android和Flash — 字幕問題

WebVTT的GetLine未遵守 &lt;cr>&lt;lf> 調整封包的長度；最後一個註解可能包含先前註解的字元。

* PTPLAY-6243 — 增強參考播放器以擷取偵錯資訊

Android範例參考播放器已增強，並包含開啟偵錯記錄檔及透過電子郵件傳送結果的選項。 可在參考播放器的「記錄」功能表下找到此選項。

**版本1.4.9 (1332)**

* Zendesk #2649 — 緩衝完成發生在初始緩衝已滿之前

搜尋後，可能是視訊引擎在視訊簡報者準備播放前將狀態設定為「正在播放」的情況。 搜尋前緩衝區狀態為高時發生。 將低緩衝狀態通知視訊引擎以進行修正。 在視訊引擎低緩衝狀態時，呼叫Play會導致狀態變更為BUFFERING而非PLAYING。 當狀態變更為「正在播放」時，繼續播放。

* Zendesk #2846 — 增強功能請求：提供為Auditude程式庫進行的呼叫設定不同使用者代理字串的功能

已新增新的API，以設定廣告相關呼叫的使用者代理程式auditudeSettings.setUserAgent(&quot;user/agent&quot;)。 如果未設定使用者代理程式，則會使用預設值。 這只會影響廣告相關呼叫的使用者代理，而媒體呼叫的使用者代理不會變更，即「Adobe Primetime」+&lt;default useragent=&quot;&quot;>.

**版本1.4.8 (1324)**

* Zendesk #1218 - 106000.33本機錯誤……如果載入PagementedHTTPStreamer：：ThreadParseManifest()中的資訊清單失敗，請檢查URL網域是否為localhost，如果是，請將網域變更為127.0.0.1，並叫用ThreadParseManifest。
* Zendesk #3072 — 自動切換至較低的位元速率。 變更緩衝區長度計算，以略過零PTS裝載。
* Zendesk #3168 — 僅在前10秒顯示WebVTT字幕。
* Zendesk #3193 — 已新增TVSDK PlaybackEventListener.onProfileChanged()中的設定檔變更API請求。

**版本1.4.7 (1311)**

* Zendesk #2197 — 追蹤廣告錯誤。 已新增資產無法載入資訊清單的通知
* Zendesk #2575 - PSDK在視訊之前會忽略MARK自訂串流內廣告
* Zendesk #2719 — 使用auditude廣告獲勝，當重新導向至auditude外掛程式中的相對url時修復了信標追蹤
* Zendesk #2760 — 在TrickPlay模式中忽略DISCONTINUITY標籤
* Zendesk #2805 — 播放開始時發生播放器當機，與Zendesk #2719的相同修正
* Zendesk #2817 - Android播放器 — 播放器有時會暫停或停止播放，將解碼緩衝區從2.0秒延長至3.0秒即可解決
* Zendesk #2839 - Adobe Primetime PSDK是否支援ARMv8晶片組？針對Galaxy S6上的當機新增修正。
* Zendesk #2885 - Auditude當機播放，與Zendesk #2719相同的修正
* Zendesk #2895 — 播放10分鐘後即時HLS仍會失敗
* Zendesk #2925 — 有關Android dev建置(1.4.5)的意見反應，在某些裝置上，當我們佇列封包到輸入佇列時，如果PTS為負數，解碼器會進入一種奇怪的狀態，我們總是會得到未來封包的負數輸出PTS。 如果輸入的PTS為負數，則修正會設為零，以避免這個問題。
* PTPLAY-4645 — 關閉openssl中的RC4密碼支援。 已知RC4的利用漏洞。 這表示如果嘗試連線到只支援RC4的伺服器，就會失敗。

**版本1.4.6 (1282)**

* Zendesk #2192 — 在惡劣的網路狀況下，位元速率並不總是較低，可透過移除快速交換器實作來修正。
* Zendesk #2631 - Android上的阿拉伯字幕：多行文字顯示為截斷，可透過調整阿拉伯字型的字型大小來修正。
* Zendesk #2844 — 附註4和片段下載時間上的緩衝不準確。

此問題已藉由將視訊區段下載之間的延遲新增至頻寬計算中，並讓下載時間計算邏輯使用完整的請求週期時間來修正。

* Zendesk #2908 — 在Nexust 5、6和7上無法使用的阿拉伯字幕，已新增2個用於阿拉伯文字的備援字型加以修正。
* PTPLAY-4627 — 將Nielson appsdk更新至1.2.3.7版
* PTPLAY-5084 — 即時主要資訊清單更新容錯移轉支援

**版本1.4.5 (1248)**

* Zendesk #1757 — 僅播放音訊或播放器當機，部分視訊位元速率設定檔已修復Nexus 4和Nexus 7當機
* Zendesk #2072 - AdEvent的TimedMetadata未包含完整URL，只是&quot;http&quot;
* Zendesk #2192 — 在網路狀況不佳時，位元速率並不總是較低
* Zendesk #2256 — 存取主要播放清單，更新PSDK以傳送主要播放清單上訂閱標籤的timedMetadata事件。
* Zendesk #2269 — 使用WebVTT時，畫面上同時出現兩種不同的字幕語言
* Zendesk #2417 — 播放器嘗試在播放開始前下載字幕，WebVTT使用錯誤的區段號碼變數進行區段號碼比對。 只有區段索引從零開始的媒體才會顯示錯誤。
* Zendesk #2470 — 在暫停後發生位元速率變更時，PSDK不會從「已暫停」狀態傳回。 在特殊情況下，當RestoreGPUResource （從暫停狀態還原播放器）呼叫智慧型搜尋且在此之前偵測到資料流切換時，智慧型搜尋無法完成，並導致持續緩衝。
* Zendesk #2451 — 隱藏式字幕「bottom inset」，新增「bottomInset」引數至字幕程式碼
* Zendesk #2480 — 停用HTTP 302重新導向最佳化，新增設定useRedirectedUrl屬性的支援
* Zendesk #2486 — 第三方信標
* Zendesk #2547 — 阿拉伯字幕：文字應靠右對齊

**1.4.4版(1195)**

* Zendesk #1158 — 在Huawei Valiant上播放失敗(Y301A1)
* Zendesk #1709 — 不正確的媒體大小和延伸視訊
* Zendesk #1757 — 只有在具有相同spa/pps資料的資料流之間切換設定檔後，才會播放音訊
* Zendesk #2095 - HTTP 307狀態（重新導向）會導致Adobe播放器停止播放
* Zendesk #2126 — 遺失上一個ADEVENT的TimedMetaData事件，最後一個區段後存在的訂閱標籤沒有從AVE回報給PSDK
* Zendesk #2227 - VideoEngine nativeReset和nativePause中的鎖定
* 錯誤#3921755 - OpenSSL程式庫更新至1.0.1L版

**版本1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 — 開啟和關閉隱藏式字幕
* PTPLAY-1818 — 倒帶特技播放在廣告處停止，而不是倒帶超過廣告
* PTPLAY-2736 — 先前顯示的WebVTT註解會在含有WebVTT註解的資料流完成播放時顯示在畫面上
* PTPLAY-3773 — 在廣告位置後開始串流播放時，不會播放中段廣告

**版本1.4.2**

* Zendesk #1561 - HLS使用者端容錯移轉支援(Primetime)。 將使用程式日期時間解決容錯移轉問題
* Zendesk #1590 - LoadInfo.MediaDuration一律為0 （僅限音訊時不會修正）
* Zendesk #1626 — 播放器中的潛在記憶體洩漏。 不是實際的記憶體流失，NotificationHistory儲存最後1000個通知時發生問題，這已減少到100個。
* Zendesk #2192 — 在網路狀況不佳時，位元速率並不總是較低

**版本1.4.1 (1121)**

* Zendesk #1951 - 4.0.x裝置上的VideoEngine.nativeReset()鎖定
* Zendesk #2064 — 特定Intel Android裝置上的原生當機SIGSEGV
* Zendesk #2075 - VideoEngine.nativeReleaseGPUResource在4.0.x裝置上的鎖定注意：此版本為 &#42;&#42;&#42;必填&#42;&#42;&#42; 支援Android 5.0 (Lollipop)
* Zendesk #1513 - Android Lollipop支援
* Zendesk #1709 — 不正確的媒體大小和延伸視訊
* Zendesk #1871 — 使用WebVTT字幕檢視直播串流時，WebVTT字幕偶爾會消失並重新出現
* Zendesk #1996 - PSDK 1.4.0中看不到時間軸標籤
* Zendesk #2046 — 使用PSDK 1.4.1.1113當機，修正從auditude未傳回任何廣告時的即時資料流當機
* 錯誤#3769657 — 將curl版本更新至7.38.0
* PTPLAY-1575 — 當ABR播放以純音訊資料流開始，然後切換到音訊/視訊資料流，當音訊繼續播放時，視訊永遠不會轉譯
* PTPLAY-2499 - OpenSSL更新至1.0.1j版，以解決最近的漏洞
* PTPLAY-2632 — 在Android Lollipop上完成中段廣告後，影片無法復原
* PTPLAY-2678 — 在Android Lollipop上即時長壽測試期間影片停頓

**1.4.0版**

* Zendesk #1024 — 透過資訊清單從資料流中移除廣告的功能
* Zendesk #1293 — 隱藏式字幕追蹤選擇問題。
* Zendesk #1590 - LoadInfo.MediaDuration一律為0，mediaDuration現在顯示正確的值。
* Zendesk #1629 - Galaxy S4上的廣告播放結束時，播放器/應用程式當機
* Zendesk #1674 — 未顯示ClosedCaption，遺失0x03 ETX程式碼時顯示正確的708字幕。
* PTPLAY-2157 - getter會傳回預設隱藏式字幕樣式，即使已在資料流上設定並視覺化驗證不同的樣式後也是如此。 隱藏式字幕樣式屬性現在會顯示其設定值。

## 1.4中的已知問題 {#known-issues-in}

**版本1.4.31**

* PTPLAY-16803 — 由於字幕系統需要視訊才能運作，因此隱藏式字幕無法搭配僅限音訊的內容運作。 沒有視訊，就沒有檢視區尺寸，沒有檢視區尺寸，我們就無法顯示任何註解的圖形。
* PTPLAY-1634 — 相同的訂閱標籤在不同的即時視窗中具有不同的時間戳記。 當即時視窗移動時，其中的相同標籤應具有相同的時間戳記。 但有時，即使是相同的標籤也會有不同的時間戳記。
* PTPLAY-3197 — 連續播放~1小時後，Acer Iconia裝置發生當機並出現訊號11 SIGSEGV錯誤
* PTPLAY-3310 — 使用某些較低位元速率的音訊，音訊在Acer Iconia上會變得斷斷續續
* PTPLAY-3355 — 使用4.0.x在Motorola Xoom上連續播放~1小時後發生WIN DEATH當機。
* PTPLAY-3557 — 在廣告插播時倒轉導致資料流完成
* PTPLAY-7079 - Android使用者端上的播放視窗無法搭配安全停止/硬停止運作
* 錯誤#3760144 — 某些裝置（例如Kindle Fire 7和Samsung Galaxy Nexus）上的資料流暫停時，解析度可能會移動或顯示為脈衝。 只有在近距離觀察下才能觀察到
* 錯誤#3761170 — 具有廣告的即時狀態中的seekToLocal無法搜尋回廣告內容，這是最適合將currentTime API用於即時資料流的方法
* 錯誤#3763370 — 有廣告的直播串流有時會同時顯示兩個廣告標籤，但應該只有一個。 這些廣告標籤代表相同的廣告，而且只會播放一個廣告
* 錯誤#3763373 — 在VOD資料流中搜尋經過廣告時，廣告標籤可能會短暫消失。 廣告標籤會還原，對時間軸沒有其他負面影響
* 有些裝置有已知的播放問題。 另請參閱 [1.4中的已知裝置問題](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 參考實作 — 範例應用程式中未實作特技播放
* 在某些Android TV裝置上，由於在下列轉變點重設解碼器，可以看到黑色影格：
   * 進入和退出涓涓細流模式
   * 在後期繫結音訊曲目之間切換
   * 從廣告到主要內容。

**版本1.4.23**

* 隱藏式字幕無法搭配純音訊內容使用，因為字幕系統需要視訊才能運作。 如果沒有視訊，就沒有檢視區尺寸，如果沒有檢視區尺寸，就無法顯示註解的任何圖形。
* 從1.4.23版開始，TVSDK將不再支援Gingerbread OS 2.3。這是因為TVSDK使用下列私人Android程式庫來收集使用Gingerbread OS之裝置的硬體資訊：

   * `libstagefright.so`
   * `libcutils.so`

在Android N版本中，Google已移除對這些私人程式庫的存取權。 Gingerbread作業系統目前佔全球的Android作業系統市場份額不到1%，因此1.4.23版之後，TVSDK將不再支援Gingerbread作業系統。
使用1.4.23版（包含支援Android N）或更新版本時：
* 更新您的應用程式以使用minSdkVersion 11版。
* 如果您的使用者執行的是OS 2.3，則SDK版本會低於應用程式的minSdkVersion。 系統會中止應用程式的安裝或升級。
* 如果您的使用者執行高於OS 2.3的版本，應用程式將會正確安裝。

如果您更新minSdkVersion：

* 如果您的使用者執行OS 2.3，應用程式已安裝但播放無法運作。
這適用於更新和全新安裝。
* 如果您的一般使用者執行的系統高於OS 2.3，表示應用程式已正確安裝，且內容已正確播放。

**版本1.4.22**

* 當接合輸出和接合輸入標籤彼此太近時，廣告的早期退出不適用於某些中段廣告。

**版本1.4.2**

* 在廣告插播時倒轉會造成資料流完成。

媒體播放器傳出MediaPlayer PlayerState.Complete時發生錯誤。在Trick Play倒帶操作期間，當它到達廣告邊界時。 當播放器處於特技播放模式時，請忽略此事件，否則SDK會正確處理狀態。

**1.4.0版(1086)**

* PTPLAY-1634 — 相同的訂閱標籤在不同的即時視窗中具有不同的時間戳記。 當Live Windows移動時，每個視窗中的相同標籤應該有相同的時間戳記。 不過，有時即使相同的標籤也會有不同的時間戳記。
* PTPLAY-2541 — 在中斷時與替代資料流進行多次切換後，有時會看到COMPONENT_CREATION_FAILURE
* 錯誤#3726865 — 如果MultiBitrate LBA資料流從僅限音訊的資料流開始，則切換到音訊/視訊資料流時不會顯示視訊。 從音訊/視訊資料流開始不會顯示此問題，而且可以成功地在音訊和音訊/視訊資料流之間切換
* 錯誤#3760144 — 當串流在Kindle Fire 7和Samsung Galaxy Nexus等裝置上暫停時，解析度可能會移動或顯示為脈衝。 只有在近距離觀察下才能觀察到
* 錯誤#3761170 — 具有廣告的即時狀態中的seekToLocal無法搜尋回廣告內容；最好將currentTime API用於即時資料流
* 錯誤#3763370 — 有廣告的直播串流有時會同時顯示兩個廣告標籤，但應該只有一個。 這些廣告標籤代表相同的廣告，而且只會播放一個廣告
* 錯誤#3763373 — 在VOD資料流中搜尋經過廣告時，廣告標籤可能會短暫消失。 廣告標籤會還原，對時間軸沒有其他負面影響
* 有些裝置有已知的播放問題。 如需詳細資訊，請參閱 [1.4中的已知裝置問題](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 參考實施 — 未在範例應用程式中實施特技播放。

## 1.4中的已知裝置問題 {#known-device-issues-in}

| 裝置 | 晶片組 | 問題 | 原因 | 因應措施 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR延遲是可預期的，因為它正在重新啟動解碼器。 |  |  |
| HTC Design （與HTC Design HD不同） | QSD8250 | 無法播放視訊。 傳回VIDEO_PROFILE_NOT_SUPPORTED錯誤。 | Design未提供適當的硬體解碼器。 它提供Stagefright的SW解碼器。 | 重新啟動裝置。 |
| HTC EVO 4G | QSD8650 | 沒有硬體解碼器。 | 高通沒有HW解碼器。 | 升級至Android 4.x。 |
| Kindle FireSystem 6.0版 | TI OMAP4 | 不播放HLS資料流。 AIR上的影片無法運作。 |  | 升級至系統版本6.3。 |
| Kindle Fire HD | TI OMAP4 | 可能會進入無法播放視訊的狀態。 傳回VIDEO_PROFILE_NOT_SUPPORTED和UNRECOVERABLE_ERROR錯誤。 | 當應用程式未完全關閉HW解碼器時（例如，在遇到當機後），HW解碼器會進入無法復原的狀態。 也會在裝置上的原生應用程式上發生。 | 重新啟動裝置。 |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE在多個ABR交換器後當機。 |  |  |
| 摩托羅拉雅特利克斯 | Tegra2 | 與AIR相比，AVE的整體效能問題。 音訊/視訊失去同步，視訊播放在9到15分鐘之間後凍結。 當機。 | 可能與我們在AIR上啟用的openGLES有關。 正在調查中。 |  |
| Nexus 7 （第2代） | S4Pro APQ8064 （高通） | 當影片暫停超過30分鐘時，裝置便會當機。 | 已向Google回報的裝置問題。 | 應用程式應逾時，以免出現長時間暫停狀態。 |
| Nexus S (GB) | 嗡嗡聲的鳥 | 無法使用硬體解碼器播放任何視訊。 | Nexus S中沒有以Stagefright為基礎的硬體解碼器，因此對於Android 2.3，我們使用SW解碼器。 | 升級至ICS。 |
| Nexus S (ICS) | 嗡嗡聲的鳥 | 視訊偶爾會忽隱忽現。 | 錯誤資料可能會導致解碼器進入錯誤狀態。 | 重新啟動裝置。 |
| Nook tabletAndroid作業系統： 2.3 | TI OMAP 4 | 視訊無法播放，應用程式當機。 | Stagefright在執行應用程式數次後進入不穩定狀態。 對mediaplayer：：QueryCodecs的呼叫暫停。 | 重新啟動裝置以重設狀態。 |
| Samsung Galaxy ACE | 高通MSM7227 | 無法安裝SampleMediaPlayer App。 | 使用ARM v6晶片組，而不是更常見的ARM v7晶片組。 FP/AIR不支援此裝置。 |  |
| Samsung Galaxy ACE2Android作業系統： 2.3.6 | NovaThor U8500 | 無法播放視訊。 | 此晶片組是AVE中適用於Android前置ICS的未知解碼器。 |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | 此裝置的視訊效能達不到標準。 | 硬體解碼器傳回含有錯誤PTS的解碼影格。 看來解碼器正在使用解碼時間而不是呈現時間。 |  |
| Samsung Galaxy S2 GAndroid OS： 2.3.6 | TI OMAP4 | 啟動視訊時當機。 |  | 升級至Android 2.3.7或4.x。 |
| Samsung Galaxy S3 (I747) | 高通MSM8960 | 視訊會斷斷續續地凍結並只播放音訊，然後就停止回應。 |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | 視訊會凍結。 | 正在調查。 |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | MBR轉換最多可能需要三秒鐘。 | 為了修正MBR當機，我們為每個資料流交換器重新啟動解碼器，這最多可能需要三秒。 |  |
| Samsung Galaxy Y |  | 無法安裝SampleMediaPlayer App。 | 使用ARM v6晶片組，而不是更常見的ARM v7晶片組。 FP/AIR不支援此裝置。 |  |
| Xoom | 泰格拉 | 有些畫面會因切換而掉格。 解碼器未重新啟動。 | OMXAL限制。 |  |

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
