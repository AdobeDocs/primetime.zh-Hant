---
title: TVSDK 2.1 PlayStation 4發行說明
seo-title: TVSDK 2.1 PlayStation 4發行說明
description: TVSDK 2.1 for PlayStation 4發行說明說明TVSDK 2.1 PlayStation 4中支援的功能及已知問題。
seo-description: TVSDK 2.1 for PlayStation 4發行說明說明TVSDK 2.1 PlayStation 4中支援的功能及已知問題。
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# TVSDK 2.1 PlayStation 4發行說明 {#tvsdk-playstation-release-notes}

TVSDK 2.1 for PlayStation 4發行說明說明TVSDK 2.1 PlayStation 4中支援的功能及已知問題。

## 已解決問題 {#resolved-issues}

以下是PlayStation 4的TVSDK 2.1已解決的問題：

**2.1.0.638版**

* **PTPLAY-10439:**&#x200B;當VMAP包裝函式和連結中斷時，播放器會陷入「準備」狀態(未傳送 `onComplete` 給呼叫者)。

* **PTPLAY-10179:**
   `creativeRepackaging` 現 `fallbackOnInvalidCreative` 在預設為關閉值。 此外，當標 `creativeRepackaging` 幟已設定但未提供 `creativeRepackaging``onRepackagingComplete` 格式時，會呼叫廣告的次數與廣告插播中的廣告次數相同，導致廣告插播被建立多次。

* **Zendesk #10304**:未初始化廣告活動開／關變數。 我們現在會從向量初始化變 `DataSetEntry's` 數。

* **PTPLAY-10318:**&#x200B;介紹了對背景模式的支援。
* **Zendesk # 17409:**&#x200B;當進入特技播放模式時，再回到正常播放模式，再次進入特技播放模式時，播放位置會跳轉。
* **PTPLAY-9552:**&#x200B;在剖析回應XML檔案後，現在每當沒有廣告時，都會ping錯誤碼1108。
* **PTPLAY-9551:**&#x200B;當Auditude處理後沒有廣告中斷時，CRS會呼叫 **onPrefetchComplete** ，其會降低groupCount。 由於沒有廣告插播，因此 **groupCount** 為0，遞減1。 之前 **groupCount****是uint32_t** ，因為它用來變更至最大值。 現在為 **int32_t**。

**2.1.0.621版**

* **Zendesk #4555** Instant on Memory issues leading-Loading errors - `MediaItemLoader` Fix for crash bening lease `mediaitemloader`

* **Zendesk #17223** 2.x CSAI:並非所有廣告追蹤URL都會引發
   * 有些VAST廣告反過來指出內嵌廣告遺失追蹤URL。
   * 當VAST XML廣告中有多個曝光標籤時，僅會儲存第一個曝光URL，而忽略其餘的標籤。 現在，所有印象URL都會儲存，稍後會進行Ping。
* **Zendesk #17224** PS4使用者代理將黃金時段資訊移至UAString結尾
* **Zendesk #17226** 2.x CSAI:並非所有銜接的廣告。\
   修正是指出時間軸已因insertBy或eraseBy操作而變更，並據以切換時段。

* **Zendesk #17284**
   [所有平台] 「隱藏字幕」都不會顯示。\
   HLS —— 支援VTT標 `EXT-X-MEDIA-TIME` 題檔案的標籤。

* **Zendesk #17889**&#x200B;在PS4上播放「Milky」\
   套用正確的yoffset（用於色彩轉換）

* **Zendesk #17954廣告備**&#x200B;援邏輯+處理空的廣泛\
   修正當其中一個Vast包裝函式為空時，Vast剖析器會用來繼續處理包裝函式的問題。

* **Zendesk #17807**&#x200B;無法通過空的廣場與Zendesk #3103相同

* **PS4和XBox One上的Zendesk #17865**&#x200B;備援邏輯\
   與Zendesk #3103相同

**2.1.0.591版**

* **Zendesk #3767** PS4廣告程式碼片段，處理VMAP重新導向時廣告解析失敗。
* **Zendesk #4096** PS4 CSAI:分段錯誤修正當TVSDK在廣告程式庫處理VMAP回應時，引發分段錯誤的當機問題。

* **影片結束時的Zendesk #4161** Trickplay 16x已修正當trickplay返回正常播放時發生的死鎖

* **Zendesk #4208開啟隱**&#x200B;藏字幕時的隨機當機啟用隱藏字幕時會洩漏固定記憶體

* **Zendesk #4213** PS4 CSAI:變更所有廣告相關呼叫的預設使用者代理字串使用者代理字串使用瀏覽器使用+新增黃金時段字串的相同UA字串建立

* **PTPLAY-7675** （內部）轉碼廣告不播放Creative重新封裝在VMAP或VAST回應中呼叫時失敗。 修正之處是，只從廣告中閱讀媒體，而不是在廣告大量時從資產中閱讀。

* **PTPLAY-7895** （內部）當沒有 `allowMultipleAds=false`廣告播放時，已修正參數未 `allowMultipleAds` 正確遵循的錯誤。

* **PTPLAY-7896** （內部）廣告在PS4上的播放順序不正確已修正廣告在XML回應中顯示順序不正確的問題。

* PS4 TVSDK已在小型應用程式中重新測試，而非在遊戲中。

**2.1.0.563版**

* **Zendesk #3868** TVSDK是否支援Playstation SDK 2.5 TVSDK現在已使用2.5 Playstation SDK建立。

* **Zendesk #4093** targetingPt廣告請求中的資訊金鑰值配對。\
   新增了分隔鍵／值對的新行字元。

## 支援的功能 {#supported-features}

TVSDK 2.1針對PlayStation 4支援下列功能：

**2.1.0.621版**

* 廣告備援、廣告選擇邏輯中的菊花鏈(Zendesk #3103)對於啟用備援規則的VAST廣告（創意人員）,TVSDK會將具有無效MIME類型的廣告視為空廣告，並嘗試在其位置使用備援廣告。您可以設定備援行為的某些方面

**2.1.0.538版**

* HLS VOD播放，包括播放、暫停、搜尋
* 可調式位元速率串流
* 使用Primetime DRM和Vanilla AES保護內容進行加密內容播放
* 包含預設廣告行為和廣告容錯的用戶端廣告插入
* 創意重新封裝
* WebVTT隱藏式字幕
* 立即啟動並自訂開始位置
* 快進快退的特技播放
* 302重新導向

## 有用的資源 {#helpful-resources}

* 請參閱 [Adobe Primetime學習與支援頁面的完整說明檔案](https://helpx.adobe.com/support/primetime.html) 。