---
title: TVSDK 2.1 PlayStation 4發行說明
description: PlayStation 4適用的TVSDK 2.1發行說明說明，說明TVSDK 2.1 PlayStation 4支援的功能和已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# TVSDK 2.1 PlayStation 4發行說明 {#tvsdk-playstation-release-notes}

PlayStation 4適用的TVSDK 2.1發行說明說明，說明TVSDK 2.1 PlayStation 4支援的功能和已知問題。

## 已解決問題 {#resolved-issues}

以下是適用於PlayStation 4的TVSDK 2.1已解決的問題：

**版本2.1.0.638**

* **PTPLAY-10439：**
VMAP包裝函式廣告連結中斷時，播放器卡在準備狀態（未傳送） `onComplete` 給呼叫者)。

* **PTPLAY-10179：**
  `creativeRepackaging` 和 `fallbackOnInvalidCreative` 值現在預設為關閉。 此外，當 `creativeRepackaging` 旗標已設定但無 `creativeRepackaging` 已提供格式， `onRepackagingComplete` 由於廣告插播中有廣告，因此系統多次呼叫廣告插播。

* **Zendesk #10304**：未初始化ad forveness on/off變數。 我們現在從初始化變數 `DataSetEntry's` ctor.

* **PTPLAY-10318：**
已引入對背景模式的支援。
* **Zendesk # 17409：**
進入特技播放模式，然後返回正常播放模式，然後再次進入特技播放模式時，播放位置會跳躍。
* **PTPLAY-9552：**
剖析回應XML檔案後，現在只要沒有廣告出現，就會釘選錯誤代碼1108。
* **PTPLAY-9551：**
當Auditude處理後沒有廣告插播時，CRS會呼叫 **onPrefetchComplete** 會遞減groupCount。 由於沒有廣告插播，因此 **群組計數** 為0並以1遞減。 先前 **群組計數** 為 **uint32_t** 因此過去會變更為最大值。 這是現在 **int32_t**.

**版本2.1.0.621**

* **Zendesk #4555**
立即記憶體問題導致載入錯誤 —  `MediaItemLoader` 釋放時發生當機的修正 `mediaitemloader`

* **Zendesk #17223**
2.x CSAI：並非所有廣告追蹤URL都會引發
   * 部分VAST廣告反過來指向內嵌廣告，導致遺失追蹤URL。
   * 當VAST XML的廣告中有多個曝光標籤時，只會儲存第一印象URL，並忽略其餘部分。 現在，將會儲存所有印象URL並於稍後釘選。
* **Zendesk #17224**
PS4使用者代理程式將primetime資訊移至UAString結尾
* **Zendesk #17226**
2.x CSAI：並非所有廣告都會匯入。\
  修正是指時間軸因insertBy或eraseBy操作而變更，並據此切換期間。

* **Zendesk #17284**
  [所有平台] 隱藏式字幕未顯示。\
  HLS — 支援 `EXT-X-MEDIA-TIME` VTT註解檔案的標籤。

* **Zendesk #17889**
在PS4上播放「Milky」\
  已套用正確的最小值（用於色彩轉換）

* **Zendesk #17954**
廣告遞補邏輯+處理空白vast\
  修正其中一個Vast包裝函式為空白時，Vast剖析器用來繼續處理包裝函式的問題。

* **Zendesk #17807**
無法通過空白vast與Zendesk #3103相同

* **Zendesk #17865**
PS4和XBox One的遞補邏輯\
  與Zendesk #3103相同

**版本2.1.0.591**

* **Zendesk #3767**
PS4廣告程式碼片段，處理VMAP重新導向時，廣告解析會失敗。
* **Zendesk #4096**
PS4 CSAI：分段錯誤已修正在廣告程式庫處理VMAP回應時，TVSDK擲回分段錯誤時的當機。

* **Zendesk #4161**
影片結尾的Trickplay 16x會凍結固定當點按播放恢復正常播放時發生鎖死

* **Zendesk #4208**
開啟隱藏式字幕時的隨機當機啟用隱藏式字幕時的固定記憶體流失

* **Zendesk #4213**
PS4 CSAI：變更所有廣告相關呼叫的預設使用者代理字串使用者代理字串是使用與瀏覽器相同的UA字串建立+ Primetime字串

* **PTPLAY-7675** （內部）轉碼廣告不會播放創意重新封裝在VMAP或VAST回應中呼叫時失敗。 Fix是在大量廣告的情況下，從廣告讀取媒體檔案，而非從資產讀取。

* **PTPLAY-7895** （內部）時間 `allowMultipleAds=false`，無廣告播放已修正以下錯誤： `allowMultipleAds` 未正確追蹤引數。

* **PTPLAY-7896** （內部）廣告在PS4上的播放順序不符問題已修正廣告在XML回應中的顯示順序問題。

* PS4 TVSDK已在迷你應用程式（而非遊戲）中重新測試。

**版本2.1.0.563**

* **Zendesk #3868**
TVSDK是否支援Playstation SDK 2.5此TVSDK現以2.5版Playstation SDK建置。

* **Zendesk #4093**
Pt Ads請求中的targetingInfo索引鍵值配對。\
  已新增分隔索引鍵/值組的新行字元。

## 支援的功能 {#supported-features}

TVSDK 2.1 for PlayStation 4支援下列功能：

**版本2.1.0.621**

* 廣告遞補、在廣告選擇邏輯中建立雛菊鏈(Zendesk #3103)對於已啟用遞補規則的VAST廣告（創意內容），TVSDK會將具有無效MIME型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。您可以設定遞補行為的某些方面

**版本2.1.0.538**

* HLS VOD播放，包括播放、暫停、搜尋
* 最適化位元速率串流
* 使用Primetime DRM和vanilla AES保護的內容進行加密內容播放
* 具有預設廣告行為和廣告寬恕的使用者端廣告插入
* 創意重新封裝
* WebVTT隱藏式字幕
* 使用自訂開始位置立即開啟
* 快速前進和快速倒帶的特技遊戲
* 302重新導向

## 實用資源 {#helpful-resources}

* 如需完整說明檔案，請前往 [Adobe Primetime學習與支援](https://experienceleague.adobe.com/docs/primetime.html) 頁面。
