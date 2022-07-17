---
title: 《 TVSDK 2.1 PlayStation 4發行說明》
description: 《 TVSDK 2.1 for PlayStation 4發行說明》介紹了TVSDK 2.1 PlayStation 4中支援的功能和已知問題。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# 《 TVSDK 2.1 PlayStation 4發行說明》 {#tvsdk-playstation-release-notes}

《 TVSDK 2.1 for PlayStation 4發行說明》介紹了TVSDK 2.1 PlayStation 4中支援的功能和已知問題。

## 已解決的問題 {#resolved-issues}

下面是針對PlayStation 4的TVSDK 2.1的已解決問題：

**2.1.0.638版**

* **PTPLAY-10439:**
當VMAP包裝器和連結斷開時，播放器將陷入「準備」狀態（未發送） 
`onComplete` )。

* **PTPLAY-10179:**

   `creativeRepackaging` 和 `fallbackOnInvalidCreative` 現在，預設情況下值處於關閉狀態。 另外，當 `creativeRepackaging` 已設定標誌但無 `creativeRepackaging` 格式， `onRepackagingComplete` 廣告片段被撥打的次數與廣告片段中有廣告的次數相同，導致廣告片段被多次建立。

* **森德克#10304**:adforvens on/off變數未初始化。 現在，我們從初始化變數 `DataSetEntry's` ctor。

* **PTPLAY-10318:**
介紹了對後台模式的支援。
* **Zendesk # 17409:**
進入特技播放模式後，回到正常播放模式，再進入特技播放模式，播放位置跳轉。
* **PTPLAY-9552:**
解析響應XML檔案後，現在只要沒有廣告就會ping錯誤代碼1108。
* **PTPLAY-9551:**
當審核處理後沒有廣告中斷時，CRS調用 
**在預回遷完成** 它會降低groupCount。 因為沒有廣告， **組計數** 為0，減1。 以前 **組計數** 是 **uint32_t** 因為它曾經變為最大值。 現在 **int32_t**。

**2.1.0.621版**

* **森德克#4555**
記憶體問題即時處理導致載入錯誤 —  
`MediaItemLoader` 修復在釋放時發生的崩潰 `mediaitemloader`

* **森德克#17223**
2.x CSAI:並非所有廣告跟蹤URL都觸發
   * 一些VAST廣告指向的是線內廣告，缺少跟蹤URL。
   * 當VAST XML中的廣告中有多個印模標籤時，只保存第一個印模URL，而忽略其餘。 現在，將保存所有印象，並稍後進行ping。
* **森德克#17224**
PS4用戶代理將黃金時段資訊移動到UAString的末尾
* **森德克#17226**
2.x CSAI:並不是所有的廣告。
\
   修復是指由於insertBy或eraseBy操作，時間軸已更改，並相應地執行期間切換。

* **森德克#17284**
   [所有平台] 未顯示隱藏字幕。\
   HLS — 支援 `EXT-X-MEDIA-TIME` VTT標題檔案的標籤。

* **森德克#17889**
在PS4上播放「奶奶」
\
   應用了正確的yoffset（用於顏色轉換）

* **森德克#17954**
廣告回退邏輯+處理空大
\
   如果Vast包裝中的一個為空，則Vast解析器會繼續處理包裝。

* **森德克#17807**
無法通過與Zendesk相同的空大#3103

* **森德克#17865**
PS4和XBox One上的回退邏輯
\
   與Zendesk #3103相同

**2.1.0.591版**

* **森德克#3767**
PS4 Ad代碼段，處理VMAP重定向時Ad解析失敗。
* **森德克#4096**
PS4 CSAI:當ad庫處理VMAP響應時，當TVSDK拋出分段錯誤時分段錯誤固定崩潰。

* **森德克#4161**
影片末尾的Trickplay 16x凍結當Trickplay返回正常播放時發生的固定死鎖

* **森德克#4208**
啟用隱藏字幕時隨機崩潰啟用隱藏字幕時固定記憶體洩漏

* **森德克#4213**
PS4 CSAI:更改所有與廣告相關的調用的預設用戶代理字串建立用戶代理字串時使用瀏覽器使用的相同UA字串+添加黃金時段字串

* **PTPLAY-7675** （內部）轉碼廣告在VMAP或VAST響應中調用時沒有播放Creative Repackaging失敗。 解決辦法是只從廣告中閱讀媒體，而不是在大廣告中閱讀資產。

* **PTPLAY-7895** （內部） `allowMultipleAds=false`，沒有廣告播放固定錯誤 `allowMultipleAds` 未正確跟蹤參數。

* **PTPLAY-7896** （內部）在PS4固定問題上，廣告的播放順序與XML響應中廣告的顯示順序不符。

* PS4 TVSDK在小型應用程式（而非遊戲）中重新測試。

**2.1.0.563版**

* **森德克#3868**
TVSDK是否支援Playstation SDK 2.5 TVSDK現在使用2.5 Playstation SDK構建。

* **森德克#4093**
定向Pt Ads請求中的Info鍵值對。
\
   添加了分隔鍵/值對的換行符。

## 支援的功能 {#supported-features}

TVSDK 2.1中支援PlayStation 4的以下功能：

**2.1.0.621版**

* 廣告回退，在廣告選擇邏輯中菊花鏈(Zendesk #3103)對於啟用了回退規則的VAST廣告（創意）,TVSDK將具有無效MIME類型的廣告視為空廣告，並嘗試使用回退廣告代替它。您可以配置回退行為的某些方面

**2.1.0.538版**

* HLS VOD播放，包括播放、暫停、查找
* 自適應比特率流
* 使用黃金時段DRM和香草AES保護的內容進行加密內容回放
* 客戶端和插入，包括預設廣告行為和廣告寬減
* 創意重新包裝
* WebVTT隱藏字幕
* 具有自定義起始位置的即時啟動
* 快進快退的特技遊戲
* 302重定向

## 有用的資源 {#helpful-resources}

* 請參閱以下網址的完整幫助文檔 [Adobe Primetime學習和支援](https://experienceleague.adobe.com/docs/primetime.html) 的子菜單。
