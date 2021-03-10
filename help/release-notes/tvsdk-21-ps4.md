---
title: TVSDK 2.1 PlayStation 4發行說明
description: TVSDK 2.1 for PlayStation 4發行說明說明TVSDK 2.1 PlayStation 4中支援的功能及已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# TVSDK 2.1 PlayStation 4發行說明{#tvsdk-playstation-release-notes}

TVSDK 2.1 for PlayStation 4發行說明說明TVSDK 2.1 PlayStation 4中支援的功能及已知問題。

## 已解決問題{#resolved-issues}

以下是PlayStation 4的TVSDK 2.1已解決的問題：

**2.1.0.638版**

* **PTPLAY-10439：當VMAP包裝函式**
和連結中斷時，播放器會陷入「準備」狀態(未傳送 
`onComplete` )。

* **PTPLAY-10179:**

   `creativeRepackaging` 和 `fallbackOnInvalidCreative` 值現在預設為關閉。此外，當設定`creativeRepackaging`旗標但未提供`creativeRepackaging`格式時，呼叫`onRepackagingComplete`的次數會與廣告插播中的廣告次數相同，導致建立廣告插播的次數會多次。

* **Zendesk #10304**:未初始化廣告活動開／關變數。我們現在會從`DataSetEntry's`向量初始化變數。

* **PTPLAY-10318：對背**
景模式的支援進行了介紹。
* **Zendesk # 17409:**
進入特技播放模式時，回到正常播放模式，再進入特技播放模式時，播放位置跳轉。
* **PTPLAY-9552：剖析回**
應XML檔案後，現在每當沒有廣告時，都會ping錯誤碼1108。
* **PTPLAY-9551：當Auditude處**
理後沒有廣告中斷時，CRS呼叫 
**** onPrefetchComplete它會降低groupCount。由於沒有廣告中斷，**groupCount**&#x200B;是0，並遞減1。 以前，**groupCount**&#x200B;是&#x200B;**uint32_t**，因為它用來變更至最大值。 現在為&#x200B;**int32_t**。

**2.1.0.621版**

* **Zendesk #4555記憶體問**
題即時載入錯誤- 
`MediaItemLoader` 解決當機時的問題  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI:並非所有廣告追蹤URL都會引發
   * 有些VAST廣告反過來指出內嵌廣告遺失追蹤URL。
   * 當VAST XML廣告中有多個曝光標籤時，只會儲存第一個曝光URL，而忽略其餘的標籤。 現在，所有印象URL都會儲存，稍後會進行Ping。
* **Zendesk #17224**
PS4使用者代理將黃金時段資訊移至UAString結尾
* **Zendesk #17226**
2.x CSAI:並非所有銜接的廣告。
\
   修正是指出時間軸已因insertBy或eraseBy操作而變更，並據以切換時段。

* **Zendesk #17284**
   [所有] 平台隱藏字幕不會顯示。\
   HLS —— 支援`EXT-X-MEDIA-TIME`標籤用於VTT標題檔案。

* **Zendesk #17889**
在PS4上播放「Milky」
\
   套用正確的yoffset（用於色彩轉換）

* **Zendesk #17954廣告備**
援邏輯+處理空的廣泛
\
   修正當其中一個Vast包裝函式為空時，Vast剖析器會用來繼續處理包裝函式的問題。

* **Zendesk #17807**
 Cannot beass event last與Zendesk #3103

* **PS4和XBox One上的Zendesk #17865**
備援邏輯
\
   與Zendesk #3103相同

**2.1.0.591版**

* **Zendesk #3767**
PS4廣告程式碼片段，處理VMAP重新導向時廣告解析失敗。
* **Zendesk #4096**
PS4 CSAI:分段錯誤修正當TVSDK在廣告程式庫處理VMAP回應時，引發分段錯誤時的當機問題。

* **影片結束時的Zendesk #4161**
Trickplay 16x凍結當trickplay返回正常播放時發生的固定死鎖

* **Zendesk #4208啟**
用隱藏字幕時隨機當機啟用隱藏字幕時固定記憶體洩漏

* **Zendesk #4213**
PS4 CSAI:變更所有廣告相關呼叫的預設使用者代理字串使用者代理字串是使用瀏覽器使用+新增黃金時段字串的相同UA字串建立

* **PTPLAY-7675** （內部）轉碼廣告無法播放在VMAP或VAST回應中呼叫Creative重新封裝失敗。修正之處是，只從廣告中閱讀媒體，而不是在廣告大量時從資產中閱讀。

* **PTPLAY-7895** （內部）當沒有 `allowMultipleAds=false`廣告播放未正確遵循參數 `allowMultipleAds` 的已修正錯誤。

* **PTPLAY-7896** （內部）廣告在PS4上的播放順序錯誤已修正廣告在XML回應中顯示順序不符的問題。

* PS4 TVSDK已在小型應用程式中重新測試，而非在遊戲中。

**2.1.0.563版**

* **Zendesk #3868**
TVSDK是否支援Playstation SDK 2.5 TVSDK現在已使用2.5 Playstation SDK建立。

* **Zendesk #4093**
targetingPt廣告請求中的資訊金鑰值配對。
\
   新增了分隔鍵／值對的新行字元。

## 支援的功能{#supported-features}

TVSDK 2.1針對PlayStation 4支援下列功能：

**2.1.0.621版**

* 廣告備援，廣告選擇邏輯中的菊花鏈(Zendesk #3103)
對於啟用備援規則的VAST廣告（創意人員）,TVSDK會將具有無效MIME類型的廣告視為空白廣告，並嘗試在其位置使用備援廣告。您可以設定備援行為的某些方面

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

## 實用資源{#helpful-resources}

* 請參閱[Adobe Primetime學習與支援](https://helpx.adobe.com/support/primetime.html)頁面的完整說明檔案。