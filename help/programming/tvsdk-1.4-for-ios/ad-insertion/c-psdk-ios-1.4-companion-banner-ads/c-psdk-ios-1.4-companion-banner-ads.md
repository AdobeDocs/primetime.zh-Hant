---
description: TVSDK支援伴生條幅廣告，這些廣告是線性廣告的附帶廣告，線上性廣告結束後，通常會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的伴隨橫幅。
title: 伴生橫幅廣告
exl-id: e7b0ce38-e4b0-4e10-8d76-2d43d8eff665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 伴生橫幅廣告 {#companion-banner-ads}

TVSDK支援伴生條幅廣告，這些廣告是線性廣告的附帶廣告，線上性廣告結束後，通常會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的伴隨橫幅。

顯示伴侶廣告時，請遵循以下建議：

* 嘗試在播放器佈局中顯示視頻廣告的夥伴橫幅廣告的數量。
* 僅當您的位置與其指定的高度和寬度完全匹配時，才顯示伴隨標題。

   >[!TIP]
   >
   >不要調整橫幅的大小。

* 在廣告開始後盡快呈現伴隨橫幅。
* 不要將主廣告/視頻容器與伴隨橫幅覆蓋。
* 廣告結束後繼續顯示伴隨橫幅。

   標準是顯示每個伴隨橫幅，直到您更換了此橫幅。

## 伴隨橫幅資料 {#companion-banner-data}

PTAdAsset的內容描述了一個伴隨的橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

的 `PTMediaPlayerAdStartedNotification` 通知返回 `PTAd` 包含實例 `companionAssets` 屬性（陣列） `PtAdAsset`)。
每個 `PtAdAsset` 提供有關顯示資產的資訊。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用資訊 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 寬度 </td> 
   <td colname="col2"> 配對標題的寬度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 陪同橫幅的高度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源類型 </td> 
   <td colname="col2">此伴隨標題的資源類型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:資料在HTML代碼中。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:資料是iframe URL(src)。 </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">靜態：資料是指向影像的直接URL的靜態URL。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資料 </td> 
   <td colname="col2"> 指定的類型的資料 <span class="codeph"> 資源類型</span> 這個伴隨的橫幅。 </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告 {#display-banner-ads}

要顯示橫幅廣告，您需要建立橫幅實例並允許TVSDK偵聽與廣告相關的事件。

TVSDK提供與通過以下連結的線性廣告關聯的夥伴橫幅廣告的清單： `PTMediaPlayerAdPlayStartedNotification` 通知事件。

清單可通過以下方式指定伴隨橫幅廣告：

* HTML段
* iFrame頁的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個伴侶廣告，TVSDK會指示哪些類型可用於應用程式。

1. 建立 `PTAdBannerView`  頁面上每個伴侶廣告插槽的實例。

       確保提供了以下資訊：
   
   * 為防止檢索不同大小的配對廣告，請使用一個標語實例來指定寬度和高度。
   * 標準橫幅大小。

1. 為 `PTMediaPlayerAdStartedNotification` 執行以下操作：
   1. 清除標題實例中的現有廣告。
   1. 獲取來自的伴侶廣告清單 `Ad.getCompanionAssets` `PTAd.companionAssets`。
   1. 如果伴生廣告清單不為空，則在標題實例的清單上迭代。

      每個標題實例( `PTAdAsset`)包含寬度、高度、資源類型（html、iframe或static）等資訊，以及顯示伴隨橫幅所需的資料。
   1. 如果視頻廣告沒有隨其預訂的伴侶廣告，則伴侶資產清單中不包含該視頻廣告的資料。

      要顯示獨立顯示廣告，請將邏輯添加到指令碼中，以在相應的標題實例中運行正常的DFP（發佈伺服器的按兩下）顯示廣告標籤。
   1. 將橫幅資訊發送到頁面上在適當位置顯示橫幅的功能。

      這通常是 `div`，您的函式使用 `div ID` 來顯示標題。 例如：

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
