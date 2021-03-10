---
description: TVSDK支援輔助橫幅廣告，這些廣告是線性廣告隨附的廣告，通常會線上性廣告結束後保留在頁面上。 您的應用程式負責顯示隨附線性廣告的配套橫幅。
title: 配套橫幅廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# 配套橫幅廣告{#companion-banner-ads}

TVSDK支援輔助橫幅廣告，這些廣告是線性廣告隨附的廣告，通常會線上性廣告結束後保留在頁面上。 您的應用程式負責顯示隨附線性廣告的配套橫幅。

顯示配套廣告時，請遵循下列建議：

* 嘗試呈現視訊廣告的配套橫幅廣告，以符合您播放器的版面。
* 只有當您的位置完全符合其指定的高度和寬度時，才會呈現配套橫幅。

   >[!TIP]
   >
   >請勿調整橫幅大小。

* 廣告開始後，請盡快呈現配套橫幅。
* 請勿將主廣告／視訊容器與配套橫幅覆蓋。
* 在廣告結束後，繼續顯示配套橫幅。

   標準是顯示每個配套橫幅，直到您取代此橫幅為止。

## 配套橫幅資料{#companion-banner-data}

PTAdAsset的內容描述了一個配套的橫幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`PTMediaPlayerAdStartedNotification`通知會傳回包含`companionAssets`屬性的`PTAd`例項（`PtAdAsset`的陣列）。
每個`PtAdAsset`都提供有關顯示資產的資訊。

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
   <td colname="col2"> 配套橫幅的寬度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 配套橫幅的高度（以像素為單位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資源類型 </td> 
   <td colname="col2">此配套橫幅的資源類型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:資料是以HTML程式碼表示。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:資料是iframe URL(src)。 </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">靜態：資料是靜態URL，是影像的直接URL。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 資料 </td> 
   <td colname="col2"> <span class="codeph"> resourceType</span>為此配套橫幅所指定類型的資料。 </td> 
  </tr> 
 </tbody> 
</table>

## 顯示橫幅廣告{#display-banner-ads}

若要顯示橫幅廣告，您必須建立橫幅例項，並允許TVSDK監聽廣告相關事件。

TVSDK會透過`PTMediaPlayerAdPlayStartedNotification`通知事件，提供與線性廣告相關的配套橫幅廣告清單。

清單可透過下列方式指定配套橫幅廣告：

* HTML程式碼片段
* iFrame頁面的URL
* 靜態影像或AdobeFlashSWF檔案的URL

對於每個配套廣告，TVSDK會指出您的應用程式有哪些類型。

1. 為頁面上的每個配套廣告插槽建立`PTAdBannerView`例項。

       請確定已提供下列資訊：
   
   * 為防止擷取不同大小的配套廣告，請使用指定寬度和高度的橫幅例項。
   * 標準橫幅大小。

1. 為`PTMediaPlayerAdStartedNotification`添加執行下列操作的觀察器：
   1. 清除橫幅例項中的現有廣告。
   1. 從`Ad.getCompanionAssets` `PTAd.companionAssets`取得配套廣告清單。
   1. 如果配套廣告清單不是空的，請在橫幅例項清單上重複。

      每個橫幅實例(`PTAdAsset`)都包含寬度、高度、資源類型（html、iframe或靜態），以及顯示配套橫幅所需的資料。
   1. 如果視訊廣告沒有隨附的配套廣告，則配套資產清單中不會包含該視訊廣告的資料。

      若要顯示獨立顯示廣告，請將邏輯新增至指令碼，以在適當的橫幅實例中執行一般的DFP（發佈者的DoubleClick）顯示廣告標籤。
   1. 將橫幅資訊傳送至頁面上顯示適當位置橫幅的函式。

      這通常是`div`，而您的函式使用`div ID`來顯示橫幅。 例如：

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
