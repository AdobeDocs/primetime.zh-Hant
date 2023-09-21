---
title: iOS適用的TVSDK 1.4發行說明
description: iOS適用的TVSDK 1.4發行說明說明TVSDK iOS 1.4的新增或變更專案、已解決和已知問題以及裝置問題
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6549'
ht-degree: 0%

---

# iOS適用的TVSDK 1.4發行說明 {#tvsdk-for-ios-release-notes}

iOS適用的TVSDK 1.4發行說明說明TVSDK iOS 1.4的新增或變更專案、已解決和已知問題，以及裝置問題。

## 新功能 {#new-features}

**版本1.4.45**

* 為了遵循Xcode10，TVSDK已從「`libstdc++`「至」`libc++`「，因此支援的最低版本為iOS 7。 之前是iOS 6。

**版本1.4.44**

* 此版本中沒有新功能或增強功能。

**版本1.4.43**

* 能夠在不觸發部分廣告追蹤的情況下於廣告中間加入的電視體驗。\
  範例：使用者在包含三個30秒廣告的90秒廣告插播中間（在40秒）加入。 這是插播中第二個廣告的10秒。

   * 第二個廣告會播放剩餘的持續時間（20秒），然後是第三個廣告。
   * 部分已播放廣告（第二個廣告）的廣告追蹤器不會觸發。 僅觸發第三個廣告的追蹤器。

* 在PTAdMetadata介面中新增布林型別的enableVodPreroll屬性。 屬性可用來在VoD資料流上啟用前置滾動。 如果enableVodPreroll為NO，PSDK不會播放前段。 但是，這不會對中繼磁碟機造成影響。 enableVodPreroll的預設值為YES。
* PTMediaPlayer介面的closedCaptionDisplayEnabled API自iOS v1.4.43起已標示為已棄用。 若要判斷隱藏式字幕是否適用於指定的PTMediaPlayerItem，請檢查PTMediaPlayerMediaItem的subtitlesOptions屬性。

**版本1.4.42**

此版本未新增任何新功能。 如需已修正的問題清單，請參閱已解決的問題。

**1.4.41版**

API變更：

* **isSecure**：推出新的API isSecure，保護播放器避免錄製和擲回錯誤。 預設值為true。
* **allowExternalRecording**：引入新的API以允許安全內容的Airplay映象。 Airplay映象被視為錄製，因此allowExternalRecording值必須設為「True」，以允許播放Mirroring或設為「False」，以停止播放映象，確保內容安全。 預設值為true。

**1.4.40版**

沒有新功能。

**版本1.4.39**

* iOS TVSDK已通過VHL 2.0.1和VHL 2.0.1與Nielsen的認證。
* iOS TVSDK已更新，可向新Akamai主機發出CRS請求 `primetime-a.akamaihd.net`.
* 新的主機名稱設定可大幅透過HTTP和HTTPS (SSL)提供CRS資產傳遞。

**版本1.4.36**

在iOS TVSDK中整合及認證VHL 2.0 ：降低API的複雜性，以降低VideoHeartbeatsLibrary實作中的障礙。

**版本1.4.34**

* 網路廣告資訊

  TVSDK API現在提供有關第三方VAST回應的其他資訊。 廣告ID、廣告系統和VAST廣告擴充功能提供於 `PTNetworkAdInfo` 類別可透過存取  `networkAdInfo`  屬性。 這些資訊可用於與其他Ad Analytics平台整合，例如 **Moat Analytics**.

**1.4.31版**

* **計費量度** 為因應客戶只想依使用量付款，而不論實際使用量為何，Adobe會收集使用量度，並使用這些量度來決定向客戶收費的金額。

每當TVSDK產生資料流開始事件時，播放器就會開始定期傳送HTTP訊息至Adobe的計費系統。 期間（稱為可計費期間）在標準VOD、專業VOD （啟用中段廣告）和即時內容中可能不同。 每種內容型別的預設持續時間為30分鐘，但您的Adobe合約會決定實際值。

* **CRS廣告的多CDN支援** TVSDK現在支援CRS廣告的多重CDN。 透過提供CRS廣告的FTP詳細資料，您可以指定CDN位置，而不是Adobe擁有的預設CDN （例如Akamai）。

**版本1.4.29**

在PTSDKConfig類別中，已新增forceHTTPS API。

PTSDKConfig類別提供在向Adobe Primetime ad decisioning、DRM和Video Analytics伺服器提出的請求上強制執行SSL的方法。 如需詳細資訊，請參閱 `forceHTTPS` 和 `isForcingHTTPS` 此類別上的方法。 如果資訊清單是透過HTTPS載入，TVSDK會保留HTTPS的內容使用方式，並在從該資訊清單載入任何相對URL時遵循此使用方式。

**注意**：不會修改對第三方網域（例如廣告追蹤畫素、內容和廣告URL）的要求以及類似要求，內容提供者和廣告伺服器應負責提供透過HTTPS支援的URL。

**版本1.4.18**

Primetime iOS TVSDK現在支援VPAID 2.0 Javascript創意，以提供豐富的互動式串流廣告體驗。

如需VPAID 2.0的詳細資訊，請參閱 [VPAID廣告支援](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

**版本1.4.17**

* tvOS

  TVSDK支援tvOS原生應用程式。
* 可以播放下列型別的內容：

   * VOD
   * 即時
   * AES-128
   * 替代音訊和字幕
   * fer

* 可顯示下列型別的廣告：

   * 基本
   * VAST2
   * VAST3
   * VMA

* 目前不支援下列功能：

   * Digital Rights Management(DRM)
   * 廣告橫幅
   * 電視標籤語言(TVML)

**版本1.4.13**

**注意**： Nielsen模組已從TVSDK組建中移除，TVSDK將在不久的未來以新的Nielsen整合模組進行更新。

* **廣告遞補、廣告選擇邏輯中的Daisy鏈結(Zendesk #3103)**

對於已啟用遞補規則的VAST廣告（創意內容），TVSDK會將具有無效MIME型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

如需詳細資訊，請參閱 [VAST和VMAP廣告的廣告遞補](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md).

**版本1.4.9**

* **透過替代內容取代發出中斷訊號**

在1.4 TVSDK更新中，我們目前也支援針對線性內容進入和從區域中斷回訪。 TVSDK現在可以平行處理兩個資訊清單檔案（主要和替代），以監視中斷訊號，即使替代程式設計正在取代原始程式設計時也是如此。

**版本1.4.8**

* **視訊心率程式庫(VHL)更新至1.5版**

   * 能夠連同視訊開始和/或視訊/廣告/章節開始一起傳送中繼資料作為內容資料
   * 網路流量較少 — 心率平均而言更少，且大小更小

**版本1.4.7**

* **內部部署個人化支援**

支援Adobe個人化伺服器的內部部署安裝，可自訂使用者端的個人化請求，以移至其他端點。

* **以解析度為基礎的輸出保護**

DRM原則現在可以根據裝置的「輸出保護」功能，指定允許的最高解析度。 舉例來說，「如果有HDCP，請允許播放解析度高達1080p的內容，如果沒有HDCP，請允許播放解析度高達480p的內容」。

**版本1.4.4**

* **視訊心率程式庫(VHL)更新至1.4.1.1版**

   * 新增將其他SDK或播放器中的不同分析使用案例與Adobe Analytics Video Essentials搭配的功能。
   * 已透過移除trackAdBreakStart和trackAdBreakComplete方法來最佳化廣告追蹤。 從trackAdStart和trackAdComplete方法呼叫推斷廣告插播。
   * 追蹤廣告時不再需要播放點屬性。
   * 新增對Marketing Cloud訪客ID的支援。

* **Nielsen SDK整合**

   * TVSDK現在支援傳送mTVR和MDPR ID3信標至Nielsen SDK，而不需要任何自訂整合。 若要開始使用，請下載3.1.2.19 Nielsen iOS應用程式SDK。

**1.4.0版**

* **透過替代內容取代發出中斷訊號**

   * 在1.4 TVSDK更新中，TVSDK現在也支援針對線性內容進入和從區域中斷返回。 TVSDK現在可以平行處理兩個資訊清單檔案（主要和替代），以監視中斷訊號，即使替代程式設計正在取代原始程式設計時也是如此。

* **移除/取代C3廣告**

   * 現在，不需要進行額外的準備工作，即可將新廣告動態插入即將從C3視窗中出來的隨選影片(VOD)資產。 TVSDK現在提供API來移除自訂內容範圍並動態插入新廣告。 在廣播期間播放即時/線性內容，而且會立即下拉以供隨選內容使用（沒有適當的時間來「清除」資產）的情況下，這項強大的新功能也相當實用。

## 1.4中的裝置認證與支援 {#device-certification-and-support-in}

>[!NOTE]
>
>下列功能為 **非** TVSDK支援：
>
>* 在任何平台或版本上，以慢動作執行。
>* 即時特技播放。

**版本1.4.43**

* TVSDK 1.4.43已通過iOS 11認證。

**版本1.4.29**

* TVSDK 1.4.29已通過iOS 10的認證。

**版本1.4.28**

* TVSDK 1.4.28已通過iOS 10 Beta 7認證。
* DRM支援可透過新增forceHTTPS和isForcingHTTPS API來強制HTTPS。
* 將VHL程式庫更新至1.5.8、Adobe行動程式庫更新至4.8.4，並將記錄器公用程式程式庫更新至7.0版部署目標。

**版本1.4.19**

此版本的TVSDK已通過iOS和tvOS的FairPlay支援認證。

**版本1.4.17**

* tvOS

  此版本的TVSDK支援tvOS，並已通過未加密的HLS資料流認證。

  **注意**：請記住以下編譯准則：

   * TVSDK tvOs支援僅限於非AdobeDRM加密資料流。 您必須在tvOS組建設定中移除drmNativeInterface.framework的參照。 仍支援AES加密資料流。
   * Apple要求所有Apple TV應用程式都必須啟用位元碼，因此您必須在專案設定中開啟此標幟。

## 1.4中的已解決問題 {#resolved-issues-in}

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
-->

<!-- 

Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 

-->

**版本1.4.45{#ios-tvsdk}**

* 票證#36294 - iOS TVSDK無法搭配Xcode 10運作

   * 修正XCode 10上TVSDK的編譯問題。 由於XCode 10需求，在iOS 1.4.45以上的TVSDK上建置應用程式需要最低部署目標，如iOS 7.0

* 票證#36321 — 在「正在播放」狀態的PTMediaPlayer和AVPlayer執行個體之間可搜尋範圍中觀察到的差異。
* 票證#36493- `libstdc++` iOS 12支援

   * 修正iOS 12上TVSDK的編譯問題。 在iOS 1.4.45以上的TVSDK上建置的應用程式需要最低部署目標為iOS 7.0

**版本1.4.44**

* 票證#34683 — 廣告播放進度時間為負數

   * 當廣告伺服器報告的持續時間與實際廣告內容不符時，會投入額外的檢查來處理這種情況。

* 票證#34801 — 在暫停狀態期間搜尋新位置時，currentTime和localTime未更新

   * 播放器目前的時間現在可以設為零，以備播放器處於暫停狀態時使用；先前只會在播放狀態中將目前時間設為零。

* 票證#35037 — 從訊號式廣告插入返回時，播放因錯誤URL而停止。

   * 改善針對1.4.42版本中已關閉問題#34385題提供的修正。 已新增isCanceled檢查與例外狀況處理程式碼，讓作業佇列更加健全。

**版本1.4.43**

* (ZD#32990) - iOS：在某些提示點上播放內容而非廣告。 &#39;selectedMediaOptionInMediaSelectionGroup&#39; API屬於AVPlayerItem介面，現已移至iOS 11的AVMediaSelection之下。 使用此新API後，問題已解決。
* (ZD#33683) TVSDK已從中繼資==字串中移除尾碼。 此問題已在剖析邏輯中修正。
* (ZD#33905) - iOS TVSDK會使用兩個使用者代理程式呼叫資訊清單檔案。 使用者代理問題已在第一個m3u8呼叫（全新安裝案例）中修正。 M3u8現在對所有呼叫都具有相同的使用者代理。
* (ZD#34293) — 插入在LINEAR資料流上的前段膠捲無法在iOS11上正確播放。 前置式廣告的問題已修正。
* (ZD#34684) — 套用廣告略過原則時，前段廣告影格會顯示幾秒鐘。 已引入新的API enableVodPreroll ，以停用vod播放中的前段播放。 此API的預設值為「是」。 API可確保略過主要內容中的廣告內容銜接。
* (ZD#34765) — 呼叫stop()後，仍會下載少數「傳輸資料流」區段。 增強Stop() API，避免下載額外的區段。
* (ZD#34865) — 直播串流的前段廣告在iOS上會遭截斷。 與iOS11相關並新增其他檢查以確認串流是前段或主要內容，可解決此問題。
* (ZD#35093) — 修正容錯移轉情況，其中如果資料流的主要變體在啟動時失敗（傳回404），則播放不會切換至備份資料流。

**1.4.42版(1.4.42.118)**

* (ZD#34385) — 從訊號式廣告插入傳回時，播放因錯誤URL而停止。

  增加CustomAVAssetLoaderOperations的最大並行計數，以便資訊清單讀取可以繼續執行。
* (ZD#34373) — 不允許串流記錄時，一般使用者無法串流到HDMI連線的裝置。
* (ZD#32678) - TVSDK無法在iOS上收集正確的廣告ID。

  如果VAST/VMAP重新導向，VHL Ping現在會擷取最終廣告創意的廣告ID。
* (ZD#33904) - TVSDK未針對AVAudioSessionMediaServicesWereLostNotification和AVAudioSessionMediaServicesWereResetNotification註冊AVFoundation通知。

  現在可以在播放器應用程式上註冊PTMediaServicesWereLostNotification和PTMediaServicesWereResetNotification，以便在媒體服務重設或遺失時取得通知。

* (ZD#33815) — 客戶無法在不更新應用程式的情況下更新其優先順序和標準化CRS規則。

  將getCRSRulesJsonURL和setCRSRulesJsonURL API新增至iOS TVSDK 。

**1.4.41版(1.4.41.76)**

* (ZD #34464) — 使用TVSDK 1.4.41版建置參考應用程式時發生問題

  自此版本開始，編譯iOS的TVSDK需要Xcode 9。
* (ZD #29456) — 播放開始於暫停狀態

  修正進入Airplay時視訊暫停的問題。
* (ZD #30371) — 當我們線上性資料流中插入超過2個廣告時，AdBreak開始時間會變更

  修正嘗試在Apple TV上播放內容時，導致完全無法播放的錯誤
* (ZD #32146) — 封鎖iOS 11 dev beta版時，沒有收到有關HLS Live內容的PTMediaPlayerStatusError

  使用Charles進行封鎖時，未針對HLS直播和VOD內容收到任何PTMediaPlayerStatusError （卸除連線和403）
* (ZD #29242) — 啟用廣告時，Airplay視訊播放失敗

  當廣告已啟用且AirPlay已啟用開始播放視訊時，視訊播放不會開始且不會顯示錯誤
* (ZD#33341) - DRMInterface.h會在Xcode 9中觸發組建警告

  修正DRMInterface.h中引數清單中遺漏&#39;void&#39;字詞的兩個區塊原型
* (ZD#31979) — 當它是iPhone 7/iPhone7+的iOS 10或更新版本時，不會編譯/執行

  已修正不再支援iOS 7之前的編譯IB檔案
* (ZD#32920) — 廣告插播內的空白畫面且無廣告插播完成

  當廣告插播展示廣告例項時，並且在廣告例項完成後，會顯示空白畫面
* (ZD#32509) — 停用iOS 11熒幕錄製停用iOS 11的熒幕錄製

* (ZD#33179) - iOS11上的間歇性事件失敗

  修正iOS 11的事件失敗

**1.4.40版** (1.4.40.72)

* (ZD #32465) — 播放器無法處理合併的播放清單。

  呼叫AV Foundation的finishLoadingWithError (with： Error)，以嘗試替代資料流/觸發容錯移轉。

* (ZD #31951) — 授權循環期間出現TVSDK錯誤。

  修正授權輪換問題。
* (ZD #31951) — 廣告插播內的空白畫面且無廣告插播完成。

  已處理Facebook VPAID廣告通常在單一\&amp;lt；AdParameters\&amp;gt； VAST節點中傳回多個CDATA區塊的問題。
* (ZD #33336) - [iOS] TVSDK — 未填入廣告Pod，儘管Freewheel已傳回足夠的廣告。

  在序列廣告和遞補廣告之間建立父子關係，並根據父序列和索引排序。

**版本1.4.39** (1.4.39.43)

* (ZD #32178) - iOS TVSDK版本不正確。

  記錄檔中的TVSDK版本輸出為1.0.211。輸出正確版本是固定的。

* (ZD #32199) — 延遲廣告載入 — 不會針對內容顯示影片。

  先前未初始化的本機Adbreak時間表現在會在使用前重新整理。

* (ZD #27528) — 如果次要音訊在iOS 1.2上設為非預設值，則資產開始播放後1-45秒內，視訊、音訊或兩者都會凍結。

  準備並通知處於就緒狀態的音軌。

* (ZD #30411) — 如果您選擇次要Sap語言，可能會收到未預期的結果，例如沒有音訊或音訊不正確。

  準備並通知處於就緒狀態的音軌。

* (ZD #32199) — 延遲廣告載入 — 不會針對內容顯示影片。

  先前未初始化的本機Adbreak時間表現在會在使用前重新整理。

* (ZD #27528) — 如果次要音訊在iOS 1.2上設為非預設值，則資產開始播放後1-45秒內，視訊、音訊或兩者都會凍結。

  準備並通知處於就緒狀態的音軌。

* (ZD #30411) — 如果您選擇次要Sap語言，可能會收到未預期的結果，例如沒有音訊或音訊不正確。

  準備並通知處於就緒狀態的音軌。

**版本1.4.38** (1.4.38.860)

* (ZD #29281) - iOS：將AdSystem和創作ID新增至CRS請求

根據CRS標準化規則在CRS請求中使用創意ID和AdSystem

* (ZD #29176) - PTAdPolicyDeligate satAdBreakAsWatched：position當機

由於空的AdBreak而造成當機的情況現在已處理。

* (ZD #30125) — 程式化廣告無法在iOS平台運作

新增iOS中的程式化廣告支援。

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME通知

使用即時DRM資料流的# EXT-X-PROGRAM-DATE-TIME標籤不會觸發定時中繼資料事件。

**1.4.37版(1.4.37.842)**

* (ZD #28950 ) - VOD播放問題

當串流中的# EXT-X-PLAYLIST-TYPE標籤設定為Event而非VOD時的播放問題

* (ZD #29281) - iOS：將AdSystem和創作ID新增至CRS請求

根據CRS標準化規則，在CRS請求中使用創作ID和AdSystem。

* (ZD #29462) - A&amp;E VOD中的TremorHub廣告導致iOS應用程式當機

**1.4.36版(1.4.36.835)**

* (ZD #29418) — 持續時間為0 (#EXT-X-CUE-OUT：0.000)的提示會導致iOS TVSDK停止或當機播放。

問題已修正，且播放已正確開始。

* (ZD #29462) - VOD中的廣告導致iOS TVSDK當機。

問題已修正。 iOS TVSDK引發例外狀況(AUDNetworkAdInfo：：initWithAdId)而無法處理。 此例外狀況是因為空白的廣告ID。

* (ZD #29281) — 將AdSystem和Creative ID新增至CRS請求。

在1401和1403請求中加入AdSystem和CreativeId作為新引數（所有其他引數維持不變）。

**版本1.4.35** (1.4.35.830)

* (ZD #27830) — 需要以程式設計方式判斷iOS中隱藏式字幕與字幕的差異。

TVSDK現在會顯示兩種型別，可用於篩選掉所需的註解型別。

* (ZD #29160) - TVSDK iOS上未正確插入EXT-X-CUE-OUT廣告提示。

搭配EXT-X-CUE-OUT midroll廣告正在播放中。

* (ZD #29100) — 當使用者拖曳至影片結尾時，應用程式當機。

修正了與同步相關的多次當機。

* (ZD #28785)、 (ZD #27712)和(ZD #25076) - iOS應用程式在大型直播活動中當機。

修正了與同步相關的多次當機。

**版本1.4.34** (適用於iOS 6.0+的1.4.34.815)

* (ZD# 28481) - FER中斷，因為這些FER資料流的廣告插播結尾附加了錯誤的索引鍵

對於FER資料流，廣告插播前的索引鍵會插入廣告插播結尾之後。 此問題已藉由附加 *上次檢視的金鑰* 在廣告插播結束時。

**版本1.4.33** (適用於iOS 6.0+的1.4.33.803)

* (ZD# 21701)為子帳戶啟用CRS

根據CRS後端的需求，透過傳送1401 CRS請求的原始創意URL，而不是標準化的URL來啟用。

* (ZD# 26218) - PSDKResources.bundle載入問題

此問題已透過更新資源載入以從所有可用套裝中檢視來解決。

* (ZD# 27460) Midroll第一個廣告呼叫 — POST至cdn.auditude<span></span>.com傳回403。

新的CDN帳戶無法處理POST CDN請求。 此問題已透過更新程式碼以使 `cdn.auditude.com` 廣告請求改為GET而非POST。

**版本1.4.32** (適用於iOS 6.0+的1.4.32.792)

* (ZD# 27132)支援VMAP廣告插播的小數值。

當內容未依定義的廣告插播分段時，整數會造成非預期的廣告位置。 未將十進位值轉換為整數即可解決此問題。

* (ZD# 27189)含EXT-X-DISCONTINUITY-SEQUENCE標籤的AES內容無法正確播放。

將標籤放在播放清單的開頭即可解決問題。

**1.4.31版** (適用於iOS 6.0+的1.4.31.785)

* (ZD# 24528)實作計費的TVSDK使用量度

如需詳細資訊，請參閱 [計費量度](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) TVSDK的子母畫面支援

在某些情況下，子母畫面功能無法正常運作，現已修正。

* (ZD# 25246)不正確的廣告插播訊號

此問題已透過跨變體資訊清單對齊不連續標籤來解決。

* (ZD# 26218)嘗試在使用者端的應用程式架構中加入PSDKLibrary.framework時，應用程式建置流程會變得複雜

依要求封裝PSDKLibrary.framework即可解決此問題。

* (ZD# 26364) CRS廣告的多CDN支援
<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028)iOS 10中部分資料流的播放延遲。

此問題已藉由為沒有M3U8擴充功能的資料流提供因應措施而解決。

**1.4.30版** (iOS 6.0+為1.4.30.754)

此版本中TVSDK的下列問題已解決：

* (ZD# 24180)新增自訂標頭以允許清單

新的自訂標題已新增至TVSDK允許清單。

* (ZD# 25016)設定ABR控制引數時，會隨機選取容錯移轉資料流

當在包含容錯移轉URL的資料流上為ABR設定提供initialBitrate設定時，依序維護ABR資料流即可解決此問題。 這將避免播放容錯移轉資料流而非主要資料流。

* (ZD# 25076) PTAuditudeAdResolver loadComplete當機

已修正快速啟動/停止含有廣告的多個PTMediaPlayer執行個體期間發生當機的問題。

* (ZD# 25960)沒有其他訂閱標籤觸發中繼資料變更通知廣播

當訂閱的標籤出現在資訊清單中的第一個區段之前時，系統未通知該標籤的問題已修正。

* (ZD# 26084) PSDK擲回106000.101000.-11833從上一個廣告插播轉換回娛樂內容時，找不到解碼器錯誤

當來自VMAP的最後一個廣告插播開始時間在總持續時間完成之前時，在某些情況下，直到最後一個廣告插播結束之後才會插入索引鍵。 此問題已修正。

* 視訊心率程式庫(VHL)已更新至1.5.9版，以解決下列問題：

   * (ZD #22351) VHL - Analytics：即時視訊資產持續時間

此問題已透過將assetDuration API新增到解決 `PTVideoAnalyticsTrackingMetadata` 更新即時/線性資料流的資產持續時間，並提供檢查即時資料流的邏輯。

* (ZD# 22675) VHL - Analytics：更新即時視訊資產持續時間

此問題與ZD #22351相同。

* (ZD #25908) VHL - Analytics：Adobe心率事件當機

此問題已透過更新實作以使用最新版iOS 1.5.9適用的VHL來改善穩定性和效能而解決。

* (ZD #25956) VHL - Analytics：重複播放視訊時當機

此問題與ZD #25908相同。

**版本1.4.29** (1.4.29.743)

* (ZD# 23901)未播放協力廠商廣告

移至CRS v3 URL結構，在重新封裝的URL中包含區域ID，即可解決此問題。

* (ZD #25183) tvOS和iOS上的DRM播放問題

此問題已藉由提供支援多DRM支援所需的多個關鍵標籤來解決。

* (ZD# 25334) TVSDK無法播放cDVR共用內容

透過防止TVSDK將空白字串轉換為絕對URL，此問題已解決。

* (ZD# 25347)在AVURLAsset上設定自訂HTTP標頭

已新增透過PTNetworkConfiguration類別對其區段請求的自訂標頭支援。

**版本1.4.28** (1.4.28.722)

* (ZD #24549)多個廣告追蹤呼叫

當建立多個播放器時，更新時間軸管理員以監聽特定物件的通知，即可解決此問題。

* (ZD #24758) PTManifestLogger不支援iOS 8

將記錄器公用程式程式庫更新至7.0版部署目標，即可解決此問題。

* (ZD #24775)由於廣告而延遲的資料流

正確計算事件播放清單上的持續時間漂移即可解決此問題。

* (ZD #24799)部分集數未在iOS應用程式中播放

當WebVTT檔案受到地理限制時，此問題可透過使用本機網頁伺服器來製作字幕來解決。

**版本1.4.27** (1.4.27.711) for iOS 6.0+

* (ZD #24089) — 針對長DVR串流進行廣告解析最佳化

此問題已透過新增多個最佳化來解決，以減少在即時/線性串流中處理DVR視窗所需的時間。

* (ZD #21554) — 未針對application-type = video/mp4觸發TVSDK錯誤信標

此問題可透過讓播放器ping無效資產格式上的正確錯誤追蹤URL來解決。

* (ZD #24424) - EXC_BAD_ACCESS KERN_INVALID_ADDRESS型別的當機起源於較新硬體裝置上iOS的PSDKLib內部。

已修正因取消配置的媒體播放器例項（在不同串流之間快速切換播放時）而發生的當機問題。

* (ZD #24575) — 當enableDebugLog=true時，32位元裝置上的TVSDK當機

已修正啟用記錄時導致32位元裝置當機的記錄格式問題。

**版本1.4.26** (1.4.26.702) for iOS 6.0+

* (ZD# 20213) - TVSDK FW必須針對XCode7進行動態/模組化

   * 已透過更新支援模組的程式庫修正

**版本1.4.25** (1.4.25.684) for iOS 6.0+

* (ZD #19629) — 進入Airplay到ATV 4時即時視訊暫停

此問題可在移除舊專案後但在將新專案新增至AVQueuePlayer之前新增等候時間，藉此解決。 若沒有等候時間，系統會將通知傳送至不正確的專案。

* (ZD #19856) — 預設啟用時不會顯示字幕

已修正webvtt播放清單中造成字幕無法正確顯示的問題。

* (ZD #21590) — 最新原始組建中的視訊效能和追蹤

已修正VideoAnalytics中缺少視訊長度的問題。

* (ZD #20202) — 設定自訂字幕樣式會當機iOS應用程式

此問題已藉由在設定子標題樣式時新增其他Null物件檢查來解決。

* (ZD #20709) — 視訊開始追蹤中的視訊長度回報為0

此問題與(ZD #21590)相同。

* (ZD #22280) - Analytics影片長度設為0

此問題與(ZD #21590)相同。

* (ZD #22592) - Primetime中的Airplay發生問題

此問題與(ZD #19629)相同。

* (ZD#22922) - iOS適用的手動位元速率切換

此問題已藉由提供指定最大位元速率的選項而解決。

* (ZD #23084) — 僅IPv6網路符合Apple規範

移除了Apple不建議用於IPv6相容性的符號。

**版本1.4.24** (1.4.24.661) for iOS 6.0+

* ZD #2548) - Primetime支援行動裝置上的互動式廣告 — VPAID 2.0

如果VPAID廣告無法播放，更新邏輯以取消隱藏播放器檢視，即可解決此問題。

* (ZD #20101) — 自訂章節實施在廣告播放期間引發章節開始事件

此問題已透過更新VideoAnalyticsTracker解決，以便在章節與非章節邊界之間轉換時正確偵測章節開始/完成。

* (ZD #20784) - Analytics：觸發即時視訊轉換的內容完成

此問題已藉由新增邏輯以在視訊追蹤工作階段期間手動觸發內容完成來解決。

下列程式庫已更新：

* AdobeMobile資料庫至4.10.0
* VHL資料庫至1.5.6
* VHL-Nielsen資料庫至1.6.7
* (ZD #21855) — 中段後不播放字幕

在此問題中，重複的不連續性標籤造成字幕未在中段後出現。 此問題已藉由移除彼此相鄰的不連續標籤來解決。

* (ZD #21994) - PTHLSUtils中的字串超出界限

當機最可能的原因是EXT-X-KEY的URL被引號包圍。

* ZD #22074) - AUDVAST當機在iOS上每分鐘發生一次

在1.4.23版中，已修正VAST重新導向URL中出現不安全字元所導致的當機。 不過，TVSDK仍持續略過這些廣告。

此問題已透過處理不安全字元和允許廣告播放而解決。

* (ZD #22694) - PTMediaPlayer。  檢視已被播放器隱藏

如果VPAID廣告無法播放，更新邏輯以取消隱藏播放器檢視，即可解決此問題。

**版本1.4.23** (1.4.23.641) for iOS 6.0+

* (ZD #18016) - Primetime SDK沒有回應且網路狀況不良

改善發生來自AVFoundation的嚴重錯誤時的錯誤通知，並允許應用程式處理錯誤後的重新啟動，即可解決此問題。

* (ZD #20580) - PTSpplicerManager當機

此問題已藉由提供額外保護，避免導致當機的並行問題而解決。

* (ZD #21782) - iOS錯誤碼10100

已修正在Adobe存取DRM資料流上開始播放時TVSDK傳回101000錯誤的問題。

* (ZD #21889) — 線上廣告和離線內容播放失敗

修正AES加密離線內容上的廣告後播放失敗的問題。

* (ZD #22074) - AUDVAST當機在iOS上每分鐘發生一次

改善處理URL中有無效字元的第三方VAST廣告標籤，即可解決此問題。

* (ZD #22257) - TVSDK無法播放DRM資料流

已修正在Adobe存取DRM資料流上開始播放時TVSDK傳回101000錯誤的問題。

**版本1.4.22** (1.4.22.627) for iOS 6.0+

* (ZD #18709) - iOS的TVSDK當機

已修正某些Adobe Access DRM保護的資料流發生當機的問題。

* (ZD #18850) — 根據CRS規則更新創意選擇邏輯

此問題已藉由新增.json設定檔案來指定創意選擇優先順序而解決。

* (ZD #19770) — 受保護的AES視訊摘要不再播放

已修正無法播放特定302重新導向資料流的問題。

* (ZD #19629) — 進入Airplay到ATV 4時即時視訊暫停

在Apple TV 4裝置上開啟Airplay功能後，新增即時視訊暫停的因應措施，即可解決此問題。 問題似乎是AppleTV 4問題。

* (ZD #21119) - TVSDK在廣告播放後停頓

已新增在使用廣告插入時支援具有序列IV的AES加密資料流。

* (ZD #21125) — 提早從即時/線性廣告插播返回

已新增支援，可讓使用者在廣告插播播放至完成之前從廣告插播回訪。 透過自訂資訊清單標籤指出提早傳回。

* (ZD #21224) - Airplay支援來自Akamai的代碼化串流

PTNetworkConfiguration類別已新增API，針對特定Akamai代碼化串流，將Cookie附加為區段的URL引數。

* (ZD #21287) — 無關的記錄檔

已修正某些記錄陳述式在xcode主控台中預設顯示的問題，即使停用記錄亦然。

* (ZD #21446) - TVSDK有時不會觸發廣告插播事件

在EVENT資料流上，在先前的版本組建中無法正確觸發廣告插播。 此組建解決此問題。

**1.4.21** (1.4.21.605) for iOS 6.0+

* (ZD #20749) — 遞補功能略過非空白的VAST回應；引發額外的廣告追蹤URL

後援廣告重複Ping的問題已解決。

**1.4.20** (1.4.20.590)適用於iOS 6.0+

* (ZD #18639) - TVSDK耗費過多的CPU/資源處理冗長的熱錄資產

CPU/資源使用量過高的問題已在兩個層級中解決。 首先，讓時間更新函式在全域佇列（而不是主要執行緒）上執行，以及最佳化CPU使用率，以使用先前處理和快取的m3u8剖析資訊清單。

* (ZD #19349) — 節流網路連線時會略過前段廣告。

此問題已藉由為應用程式和adMetadata提供逾時事件(requestTimeout)而解決。  adRequestTimeout API會覆寫預設的10秒逾時。

* (ZD #19446) — 即時資料流上缺少通知

允許應用程式在即時資料流上訂閱EXT-X-PROGRAM-DATE-TIME，此問題即已解決。

* (ZD #19459) — 使用PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions準備替代音訊時當機
* (ZD #19460) — 當機 —  [PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

此問題與Zendesk #19459相同。

* (ZD #19574) - TVSDK未針對DRM或非DRM內容傳回M3U8回應資料

在PTMediaPlayerItem.prepareToPlay中初始載入資訊清單檔案時，如果載入資訊清單失敗，TVSDK不會向應用程式報告失敗回應的內文。

允許TVSDK將失敗回應回報給應用程式，即可解決此問題。

* (ZD #19615) — 遞補邏輯無法運作

在目前的實作中，已略過遞補廣告，除非這些廣告為m3u8格式，否則不會重新封裝。 此問題已透過新增對重新封裝遞補廣告的支援而解決。

* (ZD #19770) - TVSDK無法透過302重新導向播放任何受保護的AES內容

已修正重新導向問題，因為重新導向URL在可用來剖析資訊清單之前已被cleanConnectionData清除。

* (ZD #19856) — 預設啟用時，某些位元速率不會顯示字幕

針對未顯示字幕的資料流區段，處理iOS的錯誤，即可解決此問題。

* (ZD #19868) — 販運無效創意時，TVSDK會當機

已修正TVSDK中錯誤解除配置Vast剖析器執行個體的當機問題。

* (ZD #20180) — 偶爾會略過VPAID廣告

JavaScript MIME型別並不一定都會包含或視為有效的MIME型別。 將JavaScript加入為有效的MIME型別即可解決此問題。

* (ZD #20749) — 遞補功能略過非空白的VAST回應；引發額外的廣告追蹤URL

已修正部分創意內容未重新封裝的問題。

**版本1.4.19** (1.4.19.563) for iOS 6.0+

* ZD #18639) - TVSDK耗費過多的CPU/資源處理冗長的熱錄資產

此問題已透過最佳化DRM m3u8播放清單重寫，以快取先前已重寫的播放清單位元來解決。 當您播放即時m3u8資料流時，此設定最相關，因為每下載一次區段後，就會下載該資料流的m3u8。

* (ZD#18956) — 在iOS示範播放器中設定中斷點時，player.drmManager為零

此問題已藉由更新PTMediaPlayer.drmManager API實作以從DRM架構選取DRManager來解決。

**版本1.4.18** 適用於iOS 6.0+的( 1.4.18.557)

* (ZD #18844)在iOS播放器中追蹤即時內容的播放點。

允許應用程式設定自己的播放點值，即可解決此問題。

* Zendesk #18518 — 如果未指定視訊名稱，TVSDK的名稱會預設為 *PSDK型播放器。*

此問題已透過移除播放器名稱的預設值來解決。

**版本1.4.17** (1.4.17.545) for iOS 6.0+

* Zendesk #2228 — 增強TVSDK以傳回擷取資訊清單的JSON回應

DRM Framework不會在內容不是M3U8時傳送錯誤，而是傳回nil DRMMetadata。 當發生M3U8_PARSER_ERROR通知時，透過新增中繼資料以公開內容來解決此問題。

* Zendesk #2231 — 擷取MediaPlayerNotification中無法使用的資訊清單時傳回錯誤

與Zendesk #2228相同的解析度

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填入巨集

已解決AuditudeSDK在追蹤URL的開頭有空格時無法傳送Ping的問題。

* Zendesk #17294 — 當機SecKeyRawSign

已解決當客戶的程式碼使用金鑰鏈結時可能當機的問題。

* Zendesk #18008 — 支援iOS8+的Cookie以支援代碼化的資料流

Akamai代碼化的資料流要求在區段請求時傳送Cookie，而此功能在iOS 7及舊版上無法執行。 從iOS 8開始，Apple已新增API允許為區段請求傳遞Cookie。 TVSDK現已提供這項支援。 已新增傳送使用者代理程式的支援（如有）。

* Zendesk #18166 - TVSDK 1.4.15使用dSYM檔案選項編譯DWARF時會發出數百個警告

所有警告已解決。

**注意**：已針對TVSDK新增tvOS相容程式庫。

**版本1.4.16** (1.4.16.1454)

* Zendesk #3875 — 播放期間索引標籤S當機

回覆CRS稽核上的OKHTTP相依性，因為TVSDK現在直接使用httpurlconnection而非curl。 此問題已透過在發出另一個JNI呼叫之前清除例外來解決。

* Zendesk #4487 — 追蹤線性內容頻道

線上性資料流播放工作階段期間，透過重新初始化視訊心率追蹤器來解決問題。

* Zendesk #17919 - Android — 內容搜尋導致心率錯誤

問題是解決當章節中有搜尋時處於錯誤狀態的心率

* Zendesk #18053 — 使用TVSDK的應用程式在Marshmallow上當機

TVSDK程式庫使用會進行YUV ->RGB色彩轉換的霓虹燈程式碼時，TVSDK在Android M作業系統上當機。 使用非Neon版本的程式碼來更新造成此問題的函式，即可解決此問題。

* Zendesk #18072 - Android M — 應用程式當機

當檢查是否支援設定檔和層級時，呼叫MediaCodecList和MediaCodecInfo API時，就會發生這種當機。 Adobe正在尋求Google的支援，以取得其他深入分析。 此問題已藉由提前載入所有轉碼器資訊來解決，以避免僅在需要轉碼器資訊時呼叫這些API。

* Zendesk #18074 — 使用Android 6.0的Nexus無法使用阿拉伯字幕

此問題已藉由提供對Android CTS字型對應的支援而解決。

**版本1.4.15** (1.4.15.512)適用於iOS 6.0+

**注意**： Nielsen模組已從TVSDK組建中移除，但TVSDK將在不久的未來以新的Nielsen整合模組更新。

* (ZD #2228) — 擷取資訊清單時傳回的錯誤，無法在MediaPlayerNotification中使用

新增中繼資料，以便在通知M3U8_PARSER_ERROR發生時公開內容。

* (ZD #4437) - Adobe Primetime SDK內的當機

修正準備字幕/替代音訊時回報的當機問題。

* (ZD #4487) — 追蹤線性內容頻道

允許線上性資料流播放工作階段期間重新初始化視訊心率追蹤器。

**版本1.4.14** (1.4.14.498) for iOS 6.0+

* (ZD #17260) - playlistManagerForURL當機

修正因並行問題造成的間歇性當機。

**版本1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` 未填入巨集

   * 如果內嵌廣告具有不良創意，將會顯示錯誤代碼400。
   * `[ERRORCODE]` 巨集將會進行URL編碼。

* (ZD #3865)心率與IMA廣告整合

修正錯誤回報視訊長度的問題。

* 更新TVSDK示範播放器以支援iOS 9

若要正確支援iOS 9，您需要設定「應用程式傳輸安全性」的例外狀況。 為了示範，ATS會完全停用。

**版本1.4.12** (1.4.12.464) for iOS 6.0+

* (ZD #4521) CRS測試使用者端和SSAI

已修正3P URL中錯誤的反向MD5。

**版本1.4.12** (1.4.12.463) for iOS 6.0+

* (ZD #2751) CSAI和CRS |增強：處理特定媒體檔案URL中的動態元素。

更新Creative重新封裝服務，以正確處理具有動態創意URL的廣告。

* (ZD #3654) 1.3.4.166之後PSDK版本中的記憶體流失

修正iOS 8.2裝置上定期播放的drmFramework中的記憶體洩漏問題

* (ZD #3988)第一次播放後重新搜尋時會略過Preroll

已修正錯誤，因此可正確停用廣告原則。

* (ZD #4017)請求iOS API強制向後搜尋播放廣告

已解決ZD#4279案的修正

* (ZD #4279) iOS和桌上型電腦上的HLS TVSDK廣告插入–302重新導向問題

修正廣告資產使用相對重新導向URL時的錯誤

**版本1.4.9** (1.4.9.427) for iOS 6.0+

* (ZD #3075)網際網路連線能力問題 — iOS

已新增通知，以偵測播放何時停止。

* (ZD #3193) TVSDK中的設定檔變更API要求

更新PTPlaybackInformation以公開更新的indicatedBitrate。 更新BITRATE_CHANGE通知，以對M3U8報告的位元速率提供更可靠的時間與精確度。

* (ZD #3324)當VMAP中沒有廣告媒體時，Primetime廣告會報告問題

支援釘選空白廣告插播追蹤URL，TVSDK現在將驗證空白廣告插播的廣告插播開始和完整Ping

**版本1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7當機完整事件重播

**版本1.4.7** (1.4.7.382)

* (ZD #2197)追蹤廣告錯誤。 已新增資產無法載入資訊清單的通知。
* (ZD #2894)播放器在播放期間發出4個頂層資訊清單請求。
* (ZD #2992)Auditude報告奇怪的持續時間與識別碼。

**版本1.4.6**(1.4.6.325)

* (ZD #2197)追蹤廣告錯誤。 已新增資產無法載入資訊清單的通知

**版本1.4.5** (1.4.5.283)

* (ZD #2141) TreeHouse應用程式的Analytics實作，新增AdobeAnalyticsPlugin.a程式庫以建置套件。
* 視訊心率程式庫更新至1.4.1.2
* (PTPALY-4226) (與ZD #2423相關)執行DRM重設可能會導致刪除應用程式檔案資料。

**版本1.4.4** (1.4.4.242)

* 視訊心率程式庫(VHL)更新至1.4.1。

* (ZD #2435)分析需求更新的TV SDK檔案

**版本1.4.2** (1.4.2.210 ： iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions傳回空白
* (ZD #2109) Primetime PSDK 1.4.1.125無法搭配Xcode 5.1.1運作
* (ZD #2137)無法載入DRM中繼資料時，iOS上的PSDK當機

**版本1.4.1** (1.4.1.125)

* (ZD #1107) CocoaLumberjack重複符號
* (ZD #1644)修改用於鎖定目標和報表的iOS使用者代理程式
* (ZD #1850) iOS SDK中包含的Cocoa Lumberjack檔案
* (ZD#1908)如果超過1個，PSDK會忽略自訂標籤

**1.4.0版** (1.4.0.32)

* Zendesk #1024 — 透過資訊清單從資料流中移除廣告的功能

## 1.4中的已知問題 {#known-issues-in}

* 在iOS TVSDK中，所有廣告都會連結至內容資訊清單。 廣告行為是透過根據內容和廣告區段的持續時間進行搜尋來實作。 因此，如果區段持續時間不準確，搜尋可能不會總是在廣告插播開始或結束的精確影格結束。 即使持續時間位於框架上，平台本身也會對搜尋施加容許度，而且可能會顯示一些框架、廣告或內容。 這是平台的限制，以及廣告插入在iOS上搭配TVSDK使用的方式。
* 在此情況下，略過的決定會發生在搜尋事件上。 不過，由於資訊清單中的廣告區段持續時間無法準確表示廣告的實際持續時間，因此搜尋的框架不正確。 因此，您會在套用廣告原則時看到一些廣告畫面。
* RECORDING_ERROR：錄製畫面時發生錯誤。
* 它可能會體驗到授權輪換影片無法在iOS 11上播放，且在iOS 9.x和iOS 10.x上可正常播放。
* 在VPAID 2.0支援中，如果透過AirPlay使用中播放，則會略過VPAID廣告。
* 當最小目標設定為iOS7 （或更新版本）時，drmNativeInterface.framework無法正確連結。\
  解決方法：明確指定 `libstdc++6`.  dylib程式庫，如下所示：前往「目標」 — >「建立階段」 — >「連結二進位檔與程式庫」並新增 `libstdc++.6.dylib`.

* 未插入用於取代API的後置廣告。
* 在廣告插播中搜尋（不退出）會發佈重複的廣告開始廣告插播通知
* 設定currentTimeUpdateInterval沒有任何效果。\
  注意：在某些iOS版本中，作業系統不會自動載入PSDKLibrary.framework內的資源。 請務必手動將PSDKResources.bundle複製到應用程式的套件資源：前往「建立階段」並複製套件資源。
* 無法使用Xcode 8或更低版本建置參考應用程式。 iOS TVSDK 1.4.41版以上，請使用Xcode 9編譯。

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html) 頁面。
