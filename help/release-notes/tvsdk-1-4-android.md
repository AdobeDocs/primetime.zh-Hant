---
title: 《 TVSDK 1.4 for Android發行說明》
description: TVSDK 1.4 for Android發行說明描述了TVSDK 1.4中的新增或更改內容、已解決和已知問題以及設備問題。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 1e3ec3b7-25be-4640-870e-928e832fe12d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# 《 TVSDK 1.4 for Android發行說明》 {#tvsdk-for-android-release-notes}

TVSDK 1.4 for Android發行說明描述了TVSDK 1.4中的新增或更改內容、已解決和已知問題以及設備問題。

## 新功能 {#new-features}

**1.4.43版**

**通過HTTPS安全廣告載入**

Adobe Primetime提供了通過HTTPS向黃金時段廣告伺服器和CRS請求首次呼叫的選項。

**alwaysUseAudioOutputLatency(boolean val)（在MediaPlayer類中）**

設定此參數後，在音頻時間戳計算中使用音頻輸出延遲。

它接受布爾參數val。 如果其值為 `True`，客戶端在音頻時間戳計算中使用音頻輸出延遲。

**1.4.42版**

**部分Ad-Break插入：**
像電視一樣的體驗，即在廣告中間加入廣告，而不為部分觀看的廣告觸發跟蹤。
示例：用戶在90秒廣告中間（40秒）加入，其中包括3個30秒廣告。 這是第二個廣告的10秒。
* 第二廣告在剩餘持續時間（20秒）後播放第三廣告。
* 不會觸發播放的部分廣告（第二個廣告）的廣告跟蹤器。 只有第三個廣告的追蹤器被發射。

**1.4.41版**

沒有新功能。

**1.4.40版**

沒有新功能。

>[!NOTE]
>
>如果API的版本早於1.4.39，則不需要更改。

**1.4.39版**

* TVSDK經VHL 2.0.1認證，VHL 2.0.1經Nielsen認證。
* 更新Android TVSDK以從新Akamai主機發出CRS請求 `primetime-a.akamaihd.net`。
* 新的主機名配置提供了通過HTTP和HTTPS(SSL)的CRS資產傳遞，其規模更大。
* TVSDK支援Android Oreo版本。
* 將新函式添加到 `AdClientFactory` 類以支援註冊多個機會檢測器：

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   這應返回一系列PlacementOpportunityDetector。 現在，您可以註冊多個機會檢測器。 例如，對於早期和退出功能，需要兩個機會檢測器 — 一個用於廣告插入，另一個用於提前退出廣告。 只有在您已實施自己的AdvertingFactory（而不是使用DefaultDascrimingfactory）時，才需要實施此新功能。 要獲取現有行為 — 您需要建立單個Opportunity Detector()函式，如createOpportunityDetector()函式中所示，然後放入陣列並返回：

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
>如果API的版本早於1.4.39，則不需要更改。

**1.4.36版**

Android上內容跳過的錯誤修復。

**1.4.35版**

* **網路廣告資訊**

   TVSDK API現在提供有關第三方VAST響應的其他資訊。 Ad ID、Ad System和VAST Ad Extensions提供在Ad Asset上的networkAdInfo屬性可訪問的NetworkAdInfo類中。 此資訊可用於與其他Ad Analytics平台整合，如 **Moat分析**。

**1.4.31版**

**CRS廣告的多CDN支援**
* 預設情況下，所有轉碼資產都將托管在Akamai上Adobe擁有的CDN上。 在最新版本中，Adobe創意重新打包服務(CRS)提供了將轉碼創意上傳到客戶指定的多個CDN的能力。
* 將新API添加到TVSDK，以在不使用預設URL時啟用指定最終的CRS建立URL。 請參閱文檔以瞭解如何使用這些新API。

**1.4.18版**
黃金時段Android TVSDK現在支援VPAID 2.0 Javascript創意，以實現豐富的流內互動廣告體驗。 有關VPAID 2.0的詳細資訊，請參見 [VPAID廣告支援](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)。

**1.4.17版**

AC-3 5.1僅在AmazonFireTV上受支援。

**1.4.11版**

* **廣告回退，廣告選擇邏輯中的菊花鏈(Zendesk #3103** 對於啟用回退規則的VAST廣告（建立性）,TVSDK將MIME類型無效的廣告視為空廣告，並嘗試使用備用廣告。 您可以配置回退行為的某些方面。

有關詳細資訊，請參見 [VAST和VMAP廣告的廣告回退](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)。

* **視頻心跳庫(VHL)已更新到1.5版**
   * 能夠將帶有視頻啟動和/或視頻/廣告/章節啟動的元資料作為上下文資料發送
   * 網路通信量減少 — 心跳平均減少，大小減小

**1.4.7版**

* **現場個性化支援**&#x200B;支援Adobe個性化伺服器的內部安裝，以自定義客戶端的個性化請求以轉到其他端點。

**1.4.6版**

* **示例AES加密(需要Flash Player版本17.0.0.134)**現在支援基於示例的AES加密。

**1.4.2版**

* **視頻心跳庫(VHL)更新到1.4.0.1版**

   * 添加了將來自其他SDK或玩家的不同分析使用案例與Adobe Analytics視頻軟體包捆綁在一起的功能。
   * 已通過刪除trackAdBreakStart和trackAdBreakComplete方法優化了廣告跟蹤。 廣告中斷是從trackAdStart和trackAdComplete方法調用中推斷出來的。
   * 跟蹤廣告時不再需要播放頭屬性。

* **尼爾森SDK整合** TVSDK現在支援將用戶跟蹤資訊發送到尼爾森軟體開發工具包，而無需任何自定義整合。

**1.4.0版**

* **具有備用內容替換的封鎖信號** 作為1.4 TVSDK更新的一部分，TVSDK現在還支援針對線性內容進行區域封鎖並返回。 TVSDK現在可以並行處理主檔案和備用檔案兩個清單檔案，以便即使在顯示替代程式時也監視封鎖信號。

* **刪除/更換C3廣告** 現在，無需進行額外的準備工作即可將新廣告動態地插入到從C3窗口發出的視頻點播(VOD)資產中。 TVSDK現在提供了一個API來刪除自定義內容範圍並動態插入新廣告。 這種功能強大的新功能在廣播期間直播/線性內容播放時也很有用，並且會立即被拉下來，作為按需內容使用，而沒有適當的時間來「清理」資產。

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，可用於偵聽新事件， `ITEM_REPLACED`。 每當MediaPlayer上替換MediaPlayer項實例時，都會調度此事件。 實現此PlaybackEventListener的客戶端應用程式必須實現或覆蓋此新方法。
* AdClientFactory在類中添加了一個新功能，用於註冊多個Opportunity檢測器：

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

## 1.4的TVSDK更改 {#tvsdk-changes}

* 介面PlaybackEventListener有一個名為onReplaceMediaPlayerItem的新方法，可以使用它來偵聽新事件ITEM_REPLACED。 每當MediaPlayer上替換MediaPlayer項實例時，都會調度此事件。 實現此PlaybackEventListener的客戶端應用程式必須實現或覆蓋此新方法。

* AdClientFactory在類中添加了一個新功能，用於註冊多個Opportunity檢測器：

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

例如，對於早期和退出功能，您需要兩個機會檢測器 — 一個用於廣告插入，另一個用於廣告早期退出。

要覆蓋此新功能，請建立單個Opportunity Detector，然後放入陣列並返回：

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4中的設備認證和支援 {#device-certification-and-support-in}

>[!NOTE]
>
>以下功能包括 **不** TVSDK中支援：
>
>* 在任何平台或版本上執行慢動作。
>* 真人秀。


**1.4.43版**

TVSDK 1.4.43已通過Android設備的認證，Android設備具有Android 6.0.1/ 7.0和8.1(Oreo)。

* **1.4.23版：**

   * TVSDK 1.4.23已通過Android N的Android設備認證。

* **1.4.18版：**

   * 黃金時段已獲Amazon火電台認證。
   * VPAID 2.0僅在Android 4.0及更高版本的設備上受支援。

## 1.4中解決的問題 {#resolved-issues-in}

>[!NOTE]
>
>我們強烈鼓勵所有使用CRS的TVSDK客戶升級到TVSDK 1.4.39或iOS和Android的最新版本。 此升級是對現有應用程式實施的直接導入替代。 升級後，在代理工具（例如，Charles）中檢查CRS建立URL請求，以驗證路徑中的版本是否反映3.1版。例如：
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**1.4.43版**

* 票證#27143 — 無法在FireTV設備上播放5.1音頻軌道

   * TVSDK現在能夠在FireTV設備上播放AC3音頻。 播放始終在立體聲中。

* 票證#33902 — 通過HTTPS安全廣告傳遞

   * Adobe Primetime提供了通過https請求黃金時段廣告伺服器和CRS的首次呼叫的選項。

* 票證#34493 — 藍芽音頻延遲

   * 已添加 `alwaysUseAudioOutputLatency` 在MediaPlayer類中，如果設定，將導致在音頻時間戳計算中使用音頻輸出延遲。

* 票證#34949 — 整合了新版本的視頻心跳庫(VHL)。

**版本1.4.42(1791)**

* 森德克#33719:FireTV 4k自適應比特率擴展緩慢。 為FireTV 4K設備添加了對ABR的支援。
* 森德克#33338:resetDRM清除應用程式的所有資料。  處理了非TVSDK線程中的異常導致TVSDK操作隊列填滿的額外案例。

**版本1.4.41(1776)**

* Zendesk #33002 - TVSDK on Fire TV的附屬資產資料。 已實施新的AdBannerAsset類，該類將將Companion資料作為List返回 &lt;adbannerasset> 和AdAsset::id現在是字串而不是長字元。
* Zendesk #32821 — 當Android Mighile播放器遇到WWE的演示時間戳(PTS)時，它將凍結。 此問題已在此版本中解決。
* Zendesk #33572 - VideoAnalyticsProvider廣告啟動崩潰。 使用VHL+Nielsen聯合SDK版本的VideoHeartapt.jar的正確組合解決了此問題。
* Zendesk #33355 — 消防電視：將第15個問題取消。 TVSDK端和客戶未提供任何修復程式在其端和第三方驗證此問題。

**版本1.4.40(1764)**

* Zendesk #33068 — 新設備上出現Amazon唇同步問題。 此版本中已修復唇同步問題。
* Zendesk #32215 - Android TVSDK 1.4.38安全問題 `[Hotlist]`。 已更新為最新的OpenSSL1.1.0和curl-7.55.1。
* Zendesk #32920 — 廣告中斷內的空白螢幕，無廣告中斷完成。 修復了VPAID容器可能進入掛起狀態並處理FacebookVPAID廣告通常在單個\&amp;lt;AdParameters\&amp;gt中返回多個CDATA塊的問題；VAST節點。

**版本1.4.39(1744)**

* Zendesk #28976 — 許可請求需要超過一秒。 當使用POST的DRM許可請求調用正在執行時，Curl會添加額外的「期望：100-continue」標頭。 已刪除TVSDK中的「期望：」標頭。
* Zendesk #27707 - CSAI環境不遵守CUE IN標籤，無法及早返回或返回內容。 為多個機會生成器提供支援。

**版本1.4.38(1722)**

* Zendesk #21590 — 最新原始版本中的視頻效能和跟蹤

在TVSDK中整合併驗證VHL 2.0，通過降低API的複雜性來降低VideoHeartbeatsLibrary實現中的障礙。

* Zendesk #29688 — 支援Android O試用版客戶。

TVSDK支援新的Android Beta版本。

**版本1.4.36(1713)**

* Zendesk #27392 - Android上的內容跳過

為了適應解密，Android TVSDK錯誤地將非幀內容的位元組範圍擴大了16個位元組。 Iframe流需要擴展，而非非iframe流則不需要擴展。

**版本1.4.34(1702)**

* Zendesk #27638 - Leak in cURL INet對象

Posix cURL INet對象在保持cURL連接中使用的共用管理器和DNS快取時被洩漏。

通過從INet解構器中刪除Posix cURL INet對象解決了此問題。

**版本1.4.33(1694)**

* **OpenSSL庫**

OpenSSL庫已使用OpenSSL 1.0.2j版進行更新。

* Zendesk #21701 — 發送1401 CRS請求的原始建立URL，而不是規範化的URL。
通過發送原始建立URL可解決此問題。

* Zendesk #25023 — 長時間視頻播放：視頻凍結、螢幕閃爍通過為CenturyLink機頂盒設備設定最大視頻格式尺寸，解決此問題。

* Zendesk #27460 — 新Akamai帳戶無法處理POSTcdn請求。
代碼已更新，以便 `cdn.auditude.com` 要求成為GET而不是POST。

* Zendesk #28245 — 當應用程式從後台進入前台時，未正確通知播放狀態。通過正確恢復播放狀態以在應用程式返回前台時播放或暫停，此問題得到解決。

**版本1.4.32(1682)**

* Zendesk #25779 — 在WebView中啟用JavaScript時，TVSDK Android 4.2及更低版本中發現的安全漏洞具有安全漏洞。 已對運行OS 4.2或更低版本的設備禁用TVSDK使用WebView。 這將禁用TVSDK中在這些設備上使用VPAID廣告。

* Zendesk #26890 - SCREEN狀態(ON/OFF)處理參考問題 播放器當Adobe視頻引擎(AVE)從SUSPENDED狀態恢復時，DefaultMediaPlayer不更新其狀態。 因此，即使AVE處於「播放」狀態，DefaultMediaPlayer仍保持為「掛起」狀態。 在從AVE接收PLAY狀態時，即使DefaultMediaPlayer的當前狀態為SUSPENDED，也將DefaultMediaPlayer狀態設定為PLAYING，從而解決了此問題。

**版本1.4.31(1675)**

* Zendesk #21974 — 由於空對象而出現的異常
   * AdIndex在空時很少遞增。 這可能是由於為前滾adBreak接收的API調用不正確所致。 已修復資料類型以避免此類異常

* Zendesk #24714 — 關閉無關的日誌記錄
   * 已更新TVSDK以關閉無關的日誌記錄

* Zendesk #24488 - Fire TV上的AV同步問題
   * 通過改進對AV解碼器線程的處理來固定。 具體而言，每當輸入或輸出幀隊列被修改時，就運行特定於幀的內容類型的解碼器線程。

* Zendesk #26551 — 修復CRS故障
   * 當請求為HEAD（http頭）時，我們不需要讀取內容，因為內容為空。 儘管嘗試讀取它是可以的，但舊Android(4.0.x)在我們調用read()時掛起，而新Android在調用read()時返回正確值(-1)。 基於此，將代碼更改為不讀取「head」的內容

* 訪問TrickPlayManager時#26696空指針異常
   * 通過檢查TrickPlayManager對象在使用前是否不為null來修復。

**版本1.4.30(1659)**

* Zendesk #22675資產持續時間不會為即時/線性流更新此問題通過在PTVideoAnalyticsTrackingMetadata中提供新的API assetDuration來解決，該API為即時和線性流提供資產持續時間。

* Zendesk #25853切換頻道時TVSDK記憶體洩漏MediaPlayer在下載檔案時重置或釋放檔案讀取緩衝區洩漏的問題已解決。

**版本1.4.29(1653)**

* Zendesk #21200 — 當應用程式處於後台時，播放器不會從掛起狀態恢復當流切換被信號通知後播放器被掛起時，解析度允許播放器在將播放器從掛起狀態恢復時執行流切換，而不是恢復到先前位置。

* Zendesk #23412 — 如果您在廣告中斷的最後3秒內按一下任何廣告，則播放器會陷入黑匣子。此問題與Zendesk #21200相同。

* Zendesk #23616 — 將來跳過廣告中斷尋道太遠根據廣告插入類型（插入/替換）,TVSDK確定廣告持續時間是否用於計算以確定廣告中斷終點。

* Zendesk #25078 - Android TV STB上的TVSDK DRM記憶體洩漏DRM適配器對象的記憶體洩漏已被定位和修復。

* Zendesk #25067 - VideoEngineTimeline中崩潰發生這種情況是因為對象未正確清理，並且在對象被銷毀後調用了事件。 通過添加檢查來防止空異常，問題已得到解決。

* Zendesk #25352 — 設定自定義HTTP頭通過將新的自定義頭添加到TVSDK的允許清單來解決此問題。

* Zendesk #25617 — 即時流PTS滾動更新導致播放器中斷和記憶體崩潰此問題通過在段中間發生滾動更新時在BracementHTTPStreamer中添加PTS滾動更新處理來解決。

**版本1.4.28(1637)**

* Zendesk #23618 — 在咨詢廣告策略之前，廣告中斷事件將觸發問題解決方法是在由於adInsuration而跳過廣告時不觸發AD_BREAK_START和AD_START事件。 AD_BREAK_SKPITED事件將改為發送。

**版本1.4.27(1631)**

* Zendesk #23174 — 調整視頻大小時的效能問題通過證明新的API MediaPlayerView.setSurfaceFixedSize解決了此問題，該API允許TVSDK從MediaPlayerView訪問SurfaceHolder.setFixedSize()。

* Zendesk #24450 - TVSDK發出重複的廣告請求當經過的時間轉換為長時間，而不是雙倍，並且此問題已得到解決時，就會出現此問題。

**版本1.4.26(1627)**

* Zendesk #21436 - OpenSSL庫更新到1.0.2h版將OpenSSL庫更新到OpenSSL1.0.2h版
* Zendesk #23825 — 通過提供對androidCookie的支援，回調中未包含Cookie。

**版本1.4.25(1620)**

* Zendesk #22900 - Android參考播放器上未播放即時Adobe PrimetimeDRM流。記憶體分配問題已解決。
* Zendesk #23176 — 當應用程式嘗試播放VPAID廣告時，應用程式崩潰。由於應用程式未建立用於呈現VPAID廣告的自定義廣告視圖，因此發生了崩潰。 在沒有自定義廣告視圖時，通過忽略廣告伺服器響應中的VPAID廣告來解決此問題。

* Zendesk #23153 - SampleAES DRM流 — 在TVSDK參考播放器中停止播放此問題與Zendesk #22900相同。

**版本1.4.24(1612)**

* Zendesk #20784 — 分析：觸發即時視頻轉換的內容完成通過添加API(trackVideoComplete)來在即時/線性視頻跟蹤會話期間手動觸發內容完成來解決此問題。

* placeAdBreak/acceptAd操作期間Zendesk #21977 VideoEngineTimeline崩潰
   * 在此問題中，更新了以下庫：
      * AdobeMobile庫到4.10.0版
      * VHL庫到1.5.6版
      * VHL-Nielsen圖書館1.6.7版

在將廣告添加到接受的廣告清單之前，通過添加空複選框解決了此問題。

* Zendesk #22313使用Amilogic晶片集的STB的比特率不會超過1.2M此問題已通過預載入媒體編解碼器功能和禁用Amilogic晶片集設備的無縫交換機而得到解決。

* Zendesk #19520示例AES HLS資產未在TVSDK播放器中播放通過處理示例AES加密HLS流的多個PMT描述符，解決此問題。

**版本1.4.23(1602)**

* Zendesk #18852 — 根據CRS規則更新建立選擇邏輯通過添加JSON配置檔案來指定建立選擇優先順序，解決此問題。

* Zendesk #20861 - Android N本版本通過取消直接使用Android平台本機庫的能力，為Android N提供支援，這些本機庫不再可供運行Android N的應用程式訪問。

* Zendesk #21018 - Android N崩潰與ZD# 20861相同的解析度。

* Zendesk #21266 - VideoEngineAdapter在Invalid_Key錯誤上崩潰Invalid_Key錯誤不包括AVE的說明，因此分析文本會導致NPE。 通過在onError期間添加對說明的空檢查，在分析說明之前解決了此問題。

* Zendesk #22286 — 本機庫正在分配記憶體讀取密鑰/片段，導致崩潰在Android上嘗試同時載入具有多個密鑰的清單時發生的崩潰已修復。

**版本1.4.22(1581)**

* Zendesk #17236 — 使用DRM的HLS視頻的不可靠播放頭時間LBA流的時間跳轉已被固定，其中音頻段開始時間與視頻段開始時間不匹配。

* Zendesk #17680 - Selevision Andredo框上的視頻回放凍結此設備上的視頻解碼器在將視頻幀從輸出緩衝區出隊時，有時會返回顯著的輸出時間跳轉，並且此輸出時間戳保持為高。 通過返回 *不支援視頻配置檔案* 該錯誤不會強制播放器重試同一配置檔案或選擇其他配置檔案。

* Zendesk #19074 - FFWD和REW特技播放期間視頻凍結通過添加新警告TRICKPLAY_ENDED_DUE_TO_ERROR來通知應用程式特技播放已退出，且視頻因無法恢復的錯誤而暫停，此問題已得到解決。

* Zendesk #19574 - TVSDK未返回DRM或非DRM內容的M3U8響應資料此問題通過以下方式解決：

* Zendesk #19986 — 某些設備（如Android TV）的操作行為已中斷
* 將FILE_NOT_FOUND錯誤添加到條件。
* 當錯誤來自 *未找到* 錯誤，如果響應可用，則將URL和響應與錯誤說明分開。
NVidia屏蔽OP支援引入的邏輯錯誤已被修復。 在非NVidia屏蔽設備上，即使顯示類型未知，也信任顯示安全標誌。

* Zendesk #20549 — 處理過時的播放清單。 如果以前的提取未接收到新段，則通過將即時清單更新之間的間隔減少到預期段持續時間的一半，解決了此問題。

* Zendesk #20742 — 在FireTV上回放即時內容時，記憶體使用量似乎在繼續增加。崩潰是由JNI對象引用表達到限制所致。 通過刪除對在解碼器重新啟動期間建立的MediaFormat對象的引用，解決此問題。

* Zendesk #21125 — 提前從即時/線性廣告中斷(CSAI)返回。 添加了一個特徵，如果玩家通過使用剪接機會檢測器在廣告提示中註冊剪接，則允許玩家在廣告中斷期間返回主內容。

* Zendesk #21334 — 第三方廣告請求的TVSDK廣告請求超時值。 已將adRequestTimeout設定添加到AdvertisingMetadata中，該設定為廣告調用啟用全局超時。

**版本1.4.21(1566)**

* Zendesk #17781 - ADB螢幕捕獲不再工作通過添加允許螢幕捕獲的DefaultMediaPlayer.create(Context, Boolean secureSurface)API解決了此問題。
若要允許螢幕捕獲，請為secureSurface傳遞false。
重要提示：強烈建議您不要在生產設定中啟用此螢幕捕獲功能。

* Zendesk #19074 - FFWD和REW特技播放期間的視頻凍結在trickPlay可能凍結播放背景時發生的以下問題已解決：

* Zendesk #19532 — 關閉標題顯示失序
   * FHS開始變戲，但第一個幀段中沒有幀。
   * 下載iframe段時，如果FHS遇到錯誤情況，它將退出播放並暫停播放。
   * Andorid MediaCodec實現在要求刷新所有輸入/輸出緩衝區時，會永久等待輸入隊列可用性。
通過逆轉WebVTT提示的順序，使多個重疊提示顯示為「向上滾動」，解決了此問題。

* Zendesk #19574 — 在PTMediaPlayerItem.prepareToPlay中的清單檔案的初始載入中，TVSDK不返回DRM或非DRM內容的M3U8響應資料，如果載入失敗，TVSDK不向應用程式報告失敗響應的主體。
通過允許TVSDK將故障響應報告為應用程式錯誤，解決此問題。

* Zendesk #19701 — 使用SAP/不連續播放凍結已解決當音頻和視頻在不連續處未對齊時播放器凍結的問題。

* 錯誤#PTPLAY-11162 — 已解決1.0.2f版的OpenSSL庫更新。

**版本1.4.20(1546)**

* Zendesk #17384 — 功能請求：ID3元資料支援用於AAC媒體中ID3標籤的AAC播放支援已在1.4.20版中開始的Android TVSDK中提供。

* Zendesk #18358 — 播放器在位速率開關上凍結，出現不同步的間斷。通過適當處理ABR拼接邊框，解決了此問題。

* Zendesk #19232 — 使用TVSDK 1.4.18的應用程式在較舊的AmazonOS版本4上的行為異常。通過刪除TVSDK播放器初始化過程中隱藏的Web視圖建立，以避免與不支援Android Webview的設備發生衝突，解決此問題。

* Zendesk #19585 — 當發生自適應比特率轉換時進行慢速播放。
在ABR切換期間，如果新配置檔案的音頻採樣率與當前配置檔案的音頻採樣率不同，則回放將變得快速或慢速。 這是因為未通知視頻演示者音頻格式已更改。
通過確保將通知標誌設定在正確的位置，解決了此問題。

* Zendesk #19683 - SAP DAI回放 — 幾秒鐘內沒有音頻。
對於TVSDK邏輯中的幾種情況，當比較兩個格式副本段的時間戳時，RENDITION_TIMEOUT_THRESHOLD被用作可接受的值範圍，因為時間戳不能始終與0毫秒的差值匹配。 如果間隙在RENDITION_TIMEOUT_THRESHOLD的範圍內，則假定是匹配。

RENDITION_TIMEOUT_THRESHOLD已設定為100ms，但發現它對某些流是不夠的。 通過將RENDITION_TIMEOUT_THRESHOLD增加到200ms解決了此問題。

* Zendesk #19699 - TVSDK無法在VTT字幕軌道之間切換此問題已解決，方法是：在軌道更改時進行播放器轉儲並重新載入清單，並糾正影響雙位元組WebVTT字幕軌道名稱的UTF8字串轉換問題。

* Zendesk #19717 - CC選項顯示問題通過正確處理Unicode字串解決了此問題。

* Zendesk #19910 — 未檢測到TIT2 ID3標籤此問題已通過提供對ID3 v2.4字串編碼的更完整支援和對ID3 v2.3的支援而解決。

* Zendesk #20135 - TVSDK正在為VOD內容觸發多個onComplete。
通過在正確位置而不是在狀態更改事件的完全情況下添加post_roll_complete事件偵聽器來解決此問題。

**版本1.4.19(1521)**

* Zendesk #4180 - TVSDK未強制執行HDCP。
   * 這是此票證的部分修復，僅解決NVidia屏蔽設備的問題。
您必須使用Nvidia Shield中正確實現的HDCP檢測API來動態跟蹤HDCP狀態。

* Zendesk #18358 - TVSDK在不同步的位速率開關上凍結。
   * 通過添加新警告來檢測PTS中斷，並強制PTS檢查來重新搜索每個ABR交換機的正確段，解決了此問題。
要修復凍結，對mediaPlayer.setCustomConfiguration方法的調用應包括forcePTSCheckForABR作為參數。

* Zendesk #19038 - Asus Zenpad 10上沒有直播。

   此問題已通過預載入媒體編解碼器資訊而得到解決，因此您不會在運行時查詢該函式。

* 以下問題與Zendesk #19038相同：
   * Zendesk #19483 - TVSDK在英特爾平台上崩潰。
   * Zendesk #19171 - Asus Memo Pad 7上的Android 5.0崩潰。

**版本1.4.18(1503)**

* Zendesk #3324 — 當VMAP中沒有廣告媒體時，黃金時段廣告報告不會跟蹤廣告中斷。
當廣告中斷為空時，廣告中斷開始和完整跟蹤事件未被ping通。 通過在空廣告中斷（如VMAP AdBreak）上發送廣告中斷開始ping（使用有效的AdSource節點），解決此問題。

* Zendesk #18229 — 在MediaPlayer.reset()調用後忽略SetCCVisibility(VISIBLE)。通過添加setCCVisibility(Visibility.INVISIBLE)解決了此問題；到MediaPlayer類中的reset()函式。

* Zendesk #18328 -AmazonFire TV第2代設備上丟棄60FPS內容的幀問題通過將編碼的FPS應用於睡眠時間決策以及使用更好的編碼的FPS預測邏輯解決了此問題。

**版本1.4.17(1472)**

* Zendesk #2231 — 從獲取MediaPlayerNotification中不可用的清單返回錯誤通過在出現分析錯誤時包括清單的響應正文解決了此問題。

* Zendesk #17703 - VideoEngineView在視頻回放期間不會阻止螢幕截圖自API 17以來，setSecure方法已經提供，但是由於API 17涵蓋4.2 、 4.2.1和4.2.2，因此不知道哪個會引發異常，或者它是否是特定設備。 通過將VideoEngineView.setSecure包裝到try catch子句中解決了此問題。

* Zendesk #17919 — 內容查找導致心跳錯誤無效輸入資料位置錯誤是由於在預滾動之後開始查找時生成的心跳調用而發生的。 此問題已解決。

**1.4.16a** (1454a)

* Zendesk #18215 — 某些AES流無法載入。
通過在載入AES密鑰之前檢查配置檔案DRM元資料大小，解決此問題。

**版本1.4.16(1454)**

* Zendesk #3875 — 回放期間Tab S崩潰恢復OKHTTP對CRS的審核的依賴性，因為TVSDK現在直接使用httpurlconnection而不是curl。 在進行任何其他JNI呼叫之前，通過清除異常解決了此問題。

* Zendesk #4487 — 跟蹤內容的線性通道通過允許線上性流回放會話期間重新初始化視頻心跳跟蹤器，問題得到解決。

* Zendesk #17919 - Android — 內容查找導致心跳錯誤當心跳處於錯誤狀態而一章中有查找的問題已解決。

* Zendesk #18053 -Adobe Primetime在棉花糖上崩潰當TVSDK庫使用Neon代碼執行YUV ->RGB顏色轉換時，TVSDK在Android M OS上崩潰。 通過使用非neon版本的代碼更新導致此問題的函式解決了此問題。

* Zendesk #18072 - Android M — 應用程式崩潰當檢查是否支援配置檔案和級別時，調用MediaCodecList和MediaCodecInfo API時發生崩潰。 通過提前載入所有編解碼器資訊來提供臨時工作來解決該問題，以避免僅在需要編解碼器資訊時才調用這些API。

* Zendesk #18074 — 阿拉伯字幕在Nexus上與Android 6.0不相容。通過為Android提供CTS字型映射支援，問題得到瞭解決。

**1.4.15版更新(1438)**

* Zendesk #17437 - VOD內容啟動中的長延遲，帶有一些AES流。
要解決此問題，如果清單中列出多個密鑰，請並行下載所有AES密鑰。

**版本1.4.15(1435)**

* Zendesk #4278 — 當自適應比特率更改(ABR)時，Android機頂盒上出現故障。
解決方案是增加對無縫ABR交換機的支援，支援最新的Android媒體編解碼器。

* Zendesk #17063 — 調用mediaPlayer.reset()會導致視頻引擎重置錯誤。
在調度ErrorEvents時，修復程式將包括VideoEngineExceptions中的原始MediaErrorCode。

* Zendesk #17130 — 在FireTV上看到的比特率變化時，短暫而明顯的暫停。
(與上文#4278相同)修複方案是增加對無縫ABR交換機的支援，支援最新的Android媒體編解碼器。

* Zendesk #17666 — 恢復內容時附加廣告標籤、意外或無廣告。
在對視頻點播(VOD)內容執行prepareToPlay時，修復是一個問題，初始搜索在本地時間而不是虛擬時間執行。

* Zendesk #17437 - VOD內容啟動中的長延遲，帶有一些AES流。
修復是當清單中列出多個密鑰時並行下載所有AES密鑰。

* Zendesk #17851 - Android TV - ABR期間的黑幀修復是指定KEY_MAX_WIDTH和KEY_MAX_HEIGHT以啟用自適應回放。

**版本1.4.14(1415)**

* Zendesk #3875 — 播放期間Tab S崩潰。
需要額外的修復來防止崩潰。

* Zendesk #17245 - Android TV回退功能不正常。
修復了在啟用回退時播放掛起以及VMAP響應的廣告中斷為空的其他問題。

**版本1.4.14(1412)**

* Zendesk #17245 - Android TV回退功能不正常。
已刪除在回退廣告上禁用創意重新打包的限制。

**版本1.4.13(1388)**

* Zendesk #3502 — 廣告中斷期間基於HLS客戶端的故障轉移支援在廣告中斷期間發生即時配置檔案錯誤時允許故障轉移到主清單。

* Zendesk #3875 — 播放期間Tab S崩潰要解決HttpUrlConnection和cURLm之間的衝突，請使用第三方庫。

* Zendesk #4450 — 在內容解析器中為單個位置設定自定義元資料問題將setter添加到Opportunity設定。

**版本1.4.12(1388)**

* Zendesk #2751 - CSAI和CRS |增強：處理某些媒體檔案URL中的動態元素。
更新的Creative Repackaging Service以正確處理使用動態Creative URL的廣告。

* Zendesk #3965 — 從滴答播放切換回正常播放後，在開始播放之前會先跳轉一點。
   * 修復包括TVSDK，它返回在更新所有變數之前的速率更改時間，而不是嘗試計算GetStreamTime。
   * 在流的末端附近更改特技播放速度時，已修復崩潰。
   * 在特技播放期間更正了當前時間計算。

* Zendesk #3978 — 在8x和16x上進行滴答操作時經常被凍結。
   * 始終選擇位速率最低的特技播放配置檔案，以避免持續緩衝。
   * 增加跳幀間隔以實現高特技播放率。
   * 修復在特技播放期間達到目標長度後緩衝區繼續增長的問題。

* Zendesk #3992 — 額外的Trickplay速度。
TrickPlay已更新，接受高於16倍的速率；+/- 32、+/- 64和+/- 128現在也允許。

* Zendesk #4007 — 將GEOB對象解釋為時間線元資料（Android和Web）的一部分。
已添加setByteArray和getByteArray API。

* PTPLAY-7301 — 在隨機接入點啟動即時。
「即時開啟」已更新，以允許非零起始點。

**版本1.4.11(1363)**

* Zendesk #2076 — 在Motorola Xoom上使用Android 4.0.3播放視頻時經常口吃添加的設備允許清單禁止它們嘗試播放高調內容。

* 森德克#2197 - `[Ads]` 跟蹤和錯誤派遣OperationFailedEvent，並發出警告通知。

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填充宏
   * 如果內聯廣告的創作性不佳，則將顯示錯誤代碼400。
   * `[ERRORCODE]` 宏將是URL編碼

**版本1.4.10(1354)**

* Zendesk #2941 — 即時資產在可查找的範圍中沒有「0」以前，在尋求即時流的開始時有3個段緩衝區，現在可以尋找即時流的開始（即第一段的開始）。

* Zendesk #3169 — 使用Adobe Analytics整合更新參考播放器參考播放器已使用Adobe Analytics庫更新，作為示例植入。
* Zendesk #3299 — 無法解釋的特技玩耍行為
   * 修復了一個錯誤，停止特技播放後返回播放狀態可能需要幾秒鐘（有時需要25秒以上）。
   * 修復錯誤，在此錯誤中，再次在同一媒體上調用特技播放會導致流在當前時間凍結。
* Zendesk #3433 - Android和Flash — 字幕問題

GetLine for WebVTT不尊重 &lt;cr>&lt;lf> 調整資料包的長度；最後一個標題可能包含先前標題中的字元。

* PTPLAY-6243 — 增強參考播放器以捕獲調試資訊

Android示例參考玩家已得到增強，可以選擇開啟調試日誌並通過電子郵件發送結果。 此選項位於參考播放器的「日誌」菜單下。

**版本1.4.9(1332)**

* Zendesk #2649 — 初始緩衝區滿之前發生緩衝區完成

在視頻演示者準備好播放之前視頻引擎將狀態設定為「播放」的可能情況。 在查找前緩衝區狀態高時發生。 通過通知視頻引擎緩衝區狀態低來修復。 由於視頻引擎緩衝區狀態低，調用「播放」將導致狀態更改為「緩衝」，而不是「播放」。 播放狀態更改為「播放」時恢復。

* Zendesk #2846 — 增強請求：提供為Auditute庫所做調用設定不同用戶代理字串的功能

已添加新的API來設定與廣告相關的調用的用戶代理auditudeSettings.setUserAgent(&quot;user/agent&quot;)。 如果未設定用戶代理，則將使用預設代理。 這隻影響廣告相關呼叫的用戶代理，媒體呼叫的用戶代理保持不變，即為&quot;Adobe Primetime&quot;+&lt;default useragent=&quot;&quot;>。

**版本1.4.8(1324)**

* Zendesk #1218 - 106000.33本地錯誤……如果在BragementHTTPStreamer::ThreadParseManifest()中載入清單失敗，請檢查URL域是否為localhost，如果是，請將域更改為127.0.0.1並回調ThreadParseManifest。
* Zendesk #3072 — 自動切換到較低比特率。 更改緩衝區長度計算以跳過零PTS負載。
* Zendesk #3168 - WebVTT字幕僅在前10秒顯示。
* Zendesk #3193 — 已在TVSDK中請求配置檔案更改API，已添加PlaybackEventListener.onProfileChanged()。

**版本1.4.7(1311)**

* Zendesk #2197 — 跟蹤廣告錯誤。 為資產添加的通知無法載入清單
* Zendesk #2575 - PSDK在視頻前忽略MARK自定義流內廣告
* Zendesk #2719 — 使用音頻廣告獲得死亡，固定信標跟蹤在重定向到音頻插件中的相對URL時
* Zendesk #2760 — 在TrickPlay模式期間忽略的DINECTION標籤
* Zendesk #2805 — 播放開始時玩家崩潰，與Zendesk相同的修#2719
* Zendesk #2817 - Android播放器 — 播放器有時掛起並停止播放，通過將解碼緩衝區從2.0擴展到3.0秒來修復
* Zendesk #2839 -Adobe PrimetimePSDK是否支援ARMv8晶片集？在Galaxy S6上添加了崩潰修復。
* Zendesk #2885 - Auditue Borking回放，與Zendesk相同的修#2719
* Zendesk #2895 — 在回放10分鐘後始終出現Live HLS故障
* Zendesk #2925 — 在將資料包排入輸入隊列時，在某些設備上對Android開發版本(1.4.5)的反饋，如果PTS為負數，則解碼器會進入一種奇怪的狀態，即我們總是為將來的資料包得到負數的輸出PTS。 如果輸入PTS為負值，則修復程式會將其設定為零以避免此問題。
* PTPLAY-4645 — 在openssl中關閉RC4密碼支援。 RC4有已知的漏洞。 這意味著，如果嘗試與只支援RC4的伺服器連接，將失敗。

**版本1.4.6(1282)**

* Zendesk #2192 — 在網路條件較差時，比特率並不總是更低，通過刪除快速交換機實施來修復。
* Zendesk #2631 - Android上的阿拉伯文字幕：多行上的文本將被切斷，通過調整阿拉伯字型的字型大小來固定。
* Zendesk #2844 - Buffering on Note 4（注釋4）和Fragment下載時間不準確。

通過將視頻段下載之間的延遲添加到頻寬計算中並使下載時間計算邏輯使用完全請求週期時間來解決此問題。

* Zendesk #2908 — 阿拉伯文字幕在Nexust 5、6和7上不起作用，通過為阿拉伯文指令碼添加2個備用字型來修復。
* PTPLAY-4627 — 將Nielson應用程式更新到1.2.3.7版
* PTPLAY-5084 - Live Master Manifest更新故障轉移支援

**版本1.4.5(1248)**

* Zendesk #1757 — 只對某些視頻比特率配置檔案播放音頻或播放器崩潰，Nexus 4和Nexus 7崩潰已修復
* Zendesk #2072 - AdEvent的TimedMetadata不包含僅包含&quot;http&quot;的完整URL
* Zendesk #2192 — 在網路條件較差時，Bitrate並不總是較低
* Zendesk #2256 — 訪問主播放清單，更新PSDK以為主播放清單上訂閱的標籤調度timedMetadata事件。
* Zendesk #2269 - WebVTT同時在螢幕上顯示兩種不同的字幕語言
* Zendesk #2417 — 播放器在播放開始前嘗試下載字幕，WebVTT使用了錯誤的段號變數來匹配段號。 只有段索引從零開始的介質才會出現Bug。
* Zendesk #2470 — 當掛起後發生比特率更改時，PSDK不會從SUSPENDED狀態返回。 在特殊情況下，當RestoreGPUResource（從掛起狀態恢復播放器）調用智慧尋道並在此之前檢測到流切換時，智慧尋道無法完成並導致持續緩衝。
* Zendesk #2451 — 隱藏字幕「bottom inset」，將「bottomInset」參數添加到字幕代碼
* Zendesk #2480 — 禁用HTTP 302重定向優化，添加了對設定useRedirectedUrl屬性的支援
* Zendesk #2486 — 第三方信標
* Zendesk #2547 — 阿拉伯文字幕：文本應右對齊

**版本1.4.4(1195)**

* Zendesk #1158 - Huawei Valiant上播放失敗(Y301A1)
* Zendesk #1709 — 不正確的介質大小和拉伸視頻
* Zendesk #1757 — 僅在具有相同spa/pps資料的流之間進行配置檔案切換後播放音頻
* Zendesk #2095 - HTTP 307狀態（重定向）導致Adobe播放器停止播放
* Zendesk #2126 — 上個ADEVENT缺少TimedMetaData事件，在上個段之後存在的Subscribed標籤未從AVE報告給PSDK
* Zendesk #2227 - VideoEngine nativeReset和nativePause中的鎖定
* 錯誤#3921755 - OpenSSL庫更新到1.0.1L版

**版本1.4.3(1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 — 關閉和開啟字幕
* PTPLAY-1818 — 倒帶戲法在廣告上停止播放，而不是繞過廣告
* PTPLAY-2736 — 當具有WebVTT標題的流完成播放時，螢幕上會顯示先前顯示的WebVTT標題
* PTPLAY-3773 — 在廣告位置後啟動流播放時不播放中間卷廣告

**1.4.2版**

* Zendesk #1561 — 黃金時段基於HLS客戶端的故障轉移支援。 將使用程式日期時間來解決故障轉移
* Zendesk #1590 - LoadInfo.MediaDuration始終為0（非僅用於音頻）
* Zendesk #1626 — 播放器中潛在記憶體洩漏。 不是實際記憶體洩漏，NotificationHistory保存最近1000條通知時出現問題，此問題已減少到100。
* Zendesk #2192 — 在網路條件較差時，Bitrate並不總是較低

**版本1.4.1(1121)**

* Zendesk #1951 - 4.0.x設備上VideoEngine.nativeReset()中的鎖定
* Zendesk #2064 — 特定基於英特爾的Android設備上的本機崩潰SIGSEGV
* Zendesk #2075 - 4.0.x設備上VideoEngine.nativeReleaseGPUResource中的鎖定注：此版本是 &#42;&#42;&#42;要求&#42;&#42;&#42; 支援Android 5.0（棒棒糖）
* Zendesk #1513 - Android Lollipop支援
* Zendesk #1709 — 不正確的介質大小和拉伸視頻
* Zendesk #1871 - WebVTT標題在查看帶WebVTT標題的直播流時偶爾會消失，然後重新出現
* Zendesk #1996 - PSDK 1.4.0中未顯示時間線標籤
* Zendesk #2046 — 使用PSDK 1.4.1.1113時發生崩潰，當沒有從審核返回廣告時，即時流的固定崩潰
* 錯誤#3769657 — 將curl的版本更新為7.38.0
* PTPLAY-1575 — 當ABR播放僅以音頻流開始，然後切換到音頻/視頻流時，在音頻繼續時，視頻從不呈現
* PTPLAY-2499 — 將OpenSSL更新到1.0.1j版以解決最近的漏洞
* PTPLAY-2632 — 在Android Lollipop上完成中轉廣告後，視頻無法恢復
* PTPLAY-2678 - Android Lollipop上在長壽test期間視頻停止播放

**1.4.0版**

* Zendesk #1024 — 通過清單從流中刪除廣告的功能
* Zendesk #1293 — 隱藏字幕軌道選擇問題。
* Zendesk #1590 - LoadInfo.MediaDuration始終為0,mediaDuration現在顯示的值正確。
* Zendesk #1629 — 在Galaxy S4上播放廣告結束時玩家/應用崩潰
* Zendesk #1674 - ClosedCaption未顯示，當0x03 ETX代碼丟失時，將正確顯示708標題。
* PTPLAY-2157 — 即使在流上設定和直觀驗證了不同的樣式後，getter仍返回了預設的隱藏字幕樣式。 「隱藏標題」樣式屬性現在將顯示已設定的值。

## 1.4中的已知問題 {#known-issues-in}

**1.4.31版**

* PTPLAY-16803 — 由於字幕系統需要視頻才能工作，閉合字幕將不能僅使用音頻內容。 沒有視頻，就沒有視區尺寸，沒有視區尺寸，就無法顯示字幕的任何圖形。
* PTPLAY-1634 — 同一訂閱標籤在不同的即時窗口中具有不同的時間戳。 當即時窗口移動時，其中的相同標籤應具有相同的時間戳。 但是，有時，即使是相同的標籤也具有不同的時間戳。
* PTPLAY-3197 — 持續播放約1小時後，Acer Iconia設備上出現信號11 SIGSEGV錯誤時崩潰
* PTPLAY-3310 — 在較低比特率的音頻下，音頻在Acer Iconia上變得波動/震蕩
* PTPLAY-3355 — 在持續播放約1小時後，在摩托羅拉Xoom上WIN DEATH崩潰4.0.x.
* PTPLAY-3557 — 在廣告中斷時倒帶導致流完成
* PTPLAY-7079 — 安卓客戶端上的播放窗口無法與安全停止/硬停止一起使用
* 錯誤#3760144 — 在Kindle Fire 7和三星Galaxy Nexus等設備上暫停流時，解析度可能會變化，或者看起來像脈衝。 僅可觀察
* 錯誤#3761170 - SeekToLocal in Live with Ads無法重新查找廣告內容，它最好使用當前Time API用於即時流
* 錯誤#3763370 — 帶廣告的即時流偶爾會在應該只有一個廣告標籤時，將兩個廣告標籤近距離顯示。 這些廣告標籤代表同一廣告，只有一個
* 錯誤#3763373 — 在VOD流中通過廣告時，廣告標籤可能會短暫消失。 廣告標籤恢復，並且對時間線沒有其它不利影響
* 某些設備存在已知的播放問題。 請參閱 [1.4中的已知設備問題](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)。
* 參考實施 — 在示例應用程式中未實施特技播放
* 在某些Android TV設備上，由於以下過渡點處的解碼器重置，可以看到黑幀：
   * 進入和退出遊戲模式
   * 切換後綁定音軌
   * 從廣告到主要內容。

**1.4.23版**

* 由於字幕系統需要視頻才能工作，因此隱藏字幕無法處理僅音頻內容。 沒有視頻，就沒有視區尺寸，沒有視區尺寸，就無法顯示字幕的任何圖形。
* 從1.4.23版開始，TVSDK將不支援Gingerbread OS 2.3。這是因為TVSDK使用以下專用Android庫來收集有關Gingerbread OS設備的硬體資訊：

   * `libstagefright.so`
   * `libcutils.so`

在Android N版中，Google已經刪除了對這些私人庫的訪問。 目前Gingerbread作業系統在全球安卓作業系統市場中所佔的份額還不到1%，因此，在1.4.23版之後，Gingerbread作業系統將不再受TVSDK支援。
使用1.4.23版（包括對Android N的支援）或更高版本時：
* 更新應用以使用minSdkVersion 11。
* 如果最終用戶運行的是OS 2.3，則SDK版本低於應用程式的minSdkVersion。 系統中止應用程式的安裝或升級。
* 如果最終用戶運行的版本高於OS 2.3，則應用程式將正確安裝。

如果更新minSdkVersion:

* 如果最終用戶運行的是OS 2.3，則應用程式已安裝，但播放將無法工作。
這適用於更新和新安裝。
* 如果最終用戶運行的系統高於OS 2.3，則應用程式安裝正確，內容播放正確。

**1.4.22版**

* 當剪接標籤和剪接標籤彼此過於接近時，從廣告的早期退出對一些中間輥廣告不起作用。

**1.4.2版**

* 在廣告中斷時倒帶導致流完成。

媒體播放器錯誤地發送了MediaPlayer PlayerState。在特技播放倒帶操作期間，當它到達廣告邊界時完成。 玩家在特技播放模式下應忽略此事件，否則SDK將正確處理狀態。

**版本1.4.0(1086)**

* PTPLAY-1634 — 同一訂閱標籤在不同的即時窗口中具有不同的時間戳。 當即時窗口移動時，每個窗口中的相同標籤應具有相同的時間戳。 但是，有時，即使同一標籤也具有不同的時間戳。
* PTPLAY-2541 — 在封鎖期中向/從備用流進行多次切換後，有時會看到COMPONENT_CREATION_FAILURE
* 錯誤#3726865 — 如果MultiBitrate LBA流從僅音頻流開始，則如果切換到音頻/視頻流，則不會顯示視頻。 從音頻/視頻流開始將不顯示此問題，並且可以在音頻和音頻/視頻流之間成功切換
* 錯誤#3760144 — 當某些設備（如Kindle Fire 7和Samsung Galaxy Nexus）上的資料流暫停時，解析度可能會發生變化，或者看起來像是脈衝。 僅可觀察
* 錯誤#3761170 - seekToLocal in Live with Ads無法重新查找廣告內容；最好將當前Time API用於即時流
* 錯誤#3763370 — 帶廣告的即時流偶爾會在應該只有一個廣告標籤時，將兩個廣告標籤近距離顯示。 這些廣告標籤代表同一廣告，只有一個
* 錯誤#3763373 — 在VOD流中通過廣告時，廣告標籤可能會短暫消失。 廣告標籤恢復，並且對時間線沒有其它不利影響
* 某些設備存在已知的播放問題。 有關詳細資訊，請參見 [1.4中的已知設備問題](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)。
* 參考實施 — 在示例應用程式中未實施特技播放。

## 1.4中的已知設備問題 {#known-device-issues-in}

| 設備 | 晶片集 | 問題 | 原因 | 解決方法 |
|--- |--- |--- |--- |--- |
| X機器人 | TI OMAP3 | ABR延遲是預期的，因為它正在重新啟動解碼器。 |  |  |
| HTC Desire（與HTC Desire HD不同） | QSD8250 | 無法播放視頻。 返回VIDEO_PROFILE_NOT_SUPPORTED錯誤。 | Desire沒有提供正確的硬體解碼器。 給出了Stagefright的軟體解碼器。 | 重新啟動設備。 |
| HTC EVO 4G | QSD8650 | 無硬體解碼器。 | Qualcomm沒有硬體解碼器。 | 升級到Android 4.x。 |
| Kindle FireSystem 6.0版 | TI OMAP4 | 不播放HLS流。 關於AIR的視頻不起作用。 |  | 升級到系統6.3版。 |
| Kindle Fire高清 | TI OMAP4 | 可以進入無法播放視頻的狀態。 返回VIDEO_PROFILE_NOT_SUPPORTED和UNRECOVERABLE_ERROR錯誤。 | 當應用程式未完全關閉硬體解碼器（例如，在遇到崩潰後）時，硬體解碼器進入不可恢復狀態。 在設備上的本機應用上也發生。 | 重新啟動設備。 |
| Kindle Fire HD 8.9 | 長龍800 | AVE在多個ABR交換機後崩潰。 |  |  |
| 摩托羅拉·阿特麗克斯 | Tegra2 | 與AIR相比，AVE的整體效能問題。 音頻/視頻失去同步，在9到15分鐘之間播放後，視頻回放將停止。 崩潰。 | 可能與我們在AIR啟用的openGLES有關。 正在調查。 |  |
| Nexus 7（第2代） | S4Pro APQ8064(Qualcomm) | 暫停電影超過30分鐘時，設備掛起。 | 已報告給Google的設備問題。 | 應用程式應超時，以便不允許長暫停狀態。 |
| Nexus S(GB) | 《嗡嗡鳥》 | 無法使用硬體解碼器播放任何視頻。 | Nexus S中沒有基於Stagefright的硬體解碼器，因此，對於Android 2.3，我們使用的是軟體解碼器。 | 升級到ICS。 |
| Nexus S(ICS) | 《嗡嗡鳥》 | 視頻偶爾閃爍。 | 錯誤資料可能導致解碼器進入錯誤狀態。 | 重新啟動設備。 |
| Nook tabletAndroid作業系統：2.3 | TI OMAP 4 | 視頻不播放，應用掛起。 | Stagefright在運行該應用程式幾次後進入不穩定狀態。 對mediaplayer的調用：:QueryCodecs掛起。 | 重新啟動設備以重置狀態。 |
| 三星Galaxy ACE | 高通MSM7227 | 無法安裝SampleMediaPlayer應用。 | 使用ARM v6 ，而不是更常見的ARM v7晶片集。 FP/AIR不支援此設備。 |  |
| 三星Galaxy ACE2Android作業系統：2.3.6 | 新索爾U8500 | 無法播放視頻。 | 該晶片集是AVE中Android前ICS的未知解碼器。 |  |
| 三星Galaxy S2(GT-I9100) | 埃西諾斯 | 此設備的視頻效能未達到標準。 | HW解碼器用錯誤的PTS返回解碼幀。 看起來解碼器使用的是解碼時間而不是呈現時間。 |  |
| 三星Galaxy S2 GAndroid OS:2.3.6 | TI OMAP4 | 啟動視頻時崩潰。 |  | 升級到Android 2.3.7或4.x。 |
| 三星Galaxy S3(I747) | 高通MSM8960 | 間歇性地，視頻凍結，只播放音頻，然後無響應。 |  |  |
| 三星Galaxy S3 I747M | SAMSUNG_M2ATT | 視頻凍結。 | 調查。 |  |
| 三星Galaxy頁籤1 v10.1 | 泰格拉2 | MBR轉換可能需要三秒鐘。 | 作為MBR崩潰的修復程式，我們會為每個流交換機重新啟動解碼器，這最多需要三秒。 |  |
| 三星Galaxy Y |  | 無法安裝SampleMediaPlayer應用。 | 使用ARM v6 ，而不是更常見的ARM v7晶片集。 FP/AIR不支援此設備。 |  |
| 索姆 | 泰格拉 | 丟棄幾個幀以進行切換。 解碼器未重新啟動。 | OMXAL限制。 |  |

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://helpx.adobe.com/support/primetime.html) 的子菜單。
