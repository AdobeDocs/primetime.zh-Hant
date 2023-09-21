---
description: TVSDK支援隨附橫幅廣告，這是線性廣告隨附的廣告，通常線上性廣告結束後仍會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的隨附橫幅。
title: 隨附橫幅廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 隨附橫幅廣告 {#companion-banner-ads}

TVSDK支援隨附橫幅廣告，這是線性廣告隨附的廣告，通常線上性廣告結束後仍會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的隨附橫幅。

顯示隨附廣告時，請遵循下列建議：

* 嘗試儘可能多地呈現視訊廣告的隨附橫幅廣告，以符合您的播放器版面配置。
* 只有在您的位置完全符合其指定高度和寬度時，才會顯示隨附橫幅。

  >[!TIP]
  >
  >請勿調整橫幅大小。

* 在廣告開始後儘快提供隨附橫幅。
* 請勿以隨附橫幅覆蓋主要廣告/視訊容器。
* 在廣告結束後繼續顯示隨附橫幅。

  標準是顯示每個隨附橫幅，直到您有此橫幅的替代專案為止。

## 隨附橫幅資料 {#companion-banner-data}

PTAdAsset的內容會說明隨附橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `PTMediaPlayerAdStartedNotification` 通知傳回 `PTAd` 包含 `companionAssets` 屬性(陣列 `PtAdAsset`)。
每個 `PtAdAsset` 提供有關顯示資產的資訊。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>可用資訊</b></th> 
   <th colname="col2" class="entry"><b>說明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 寬度 </td> 
   <td colname="col2"> 隨附橫幅的寬度（畫素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 隨附橫幅的高度（畫素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源型別 </td> 
   <td colname="col2">此隨附橫幅的資源型別： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html：資料採用HTML程式碼。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe：資料是iframe URL (src)。 </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">靜態：資料是靜態URL，也就是影像的直接網址。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資料 </td> 
   <td colname="col2"> 指定的型別資料 <span class="codeph">resourceType</span> 以取得此隨附橫幅。 </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告 {#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK接聽與廣告相關的事件。

TVSDK提供透過與線性廣告相關的隨附橫幅廣告清單 `PTMediaPlayerAdPlayStartedNotification` 通知事件。

資訊清單可透過以下方式指定隨附橫幅廣告：

* HTML片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個隨附廣告，TVSDK會指出您的應用程式可用的型別。

1. 建立 `PTAdBannerView`  頁面上每個隨附廣告位置的例項。

       請確定已提供下列資訊：
   
   * 為了防止擷取不同大小的隨附廣告，請使用指定寬度和高度的橫幅例項。
   * 標準橫幅大小。

1. 為新增觀察者 `PTMediaPlayerAdStartedNotification` 這樣會執行下列動作：
   1. 清除橫幅例項中的現有廣告。
   1. 從取得隨附廣告清單 `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. 如果隨附廣告清單不是空的，請反複檢視橫幅例項的清單。

      每個橫幅例項( a `PTAdAsset`)包含寬度、高度、資源型別（html、iframe或靜態）等資訊，以及顯示隨附橫幅所需的資料。
   1. 如果視訊廣告沒有隨附廣告預訂，則隨附資產清單不包含該視訊廣告的資料。

      若要顯示獨立顯示廣告，請在指令碼中新增邏輯，以在適當的橫幅例項中執行一般DFP (DoubleClick for Publishers)顯示廣告標籤。
   1. 將橫幅資訊傳送至頁面上會在適當位置顯示橫幅的函式。

      這通常是 `div`，而您的函式會使用 `div ID` 以顯示橫幅。 例如：

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
