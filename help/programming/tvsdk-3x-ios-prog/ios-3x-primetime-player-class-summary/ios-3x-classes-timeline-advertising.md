---
description: 這些類提供關於時間線內發生的廣告的資訊。
title: 時間軸廣告類
exl-id: 4411c86d-8c40-457b-bfc1-40fbea77154e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 時間軸廣告類 {#timeline-advertising-classes}

這些類提供關於時間線內發生的廣告的資訊。

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>名稱</b></th> 
   <th colname="2" class="entry"><b>說明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">定義Ad抽象並包含所有Ad資訊的類。 它由唯一ID、持續時間和MediaResourcedee定義。 MediaResource包含實際廣告內容所在的URL。 
    <pre>
      表示與內容拼接的主線性資產。 它可以選擇包含必須與線性資產一起顯示的配套資產陣列。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">表示要顯示的資產的類。 
    <pre>
      表示要顯示的資產。
    </pre> 
    <pre>
      表示廣告資產的類。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      顯示標題資產。 您的應用程式必須建立此實用程式類的新實例，設定標題資產，並將其添加到視圖。 此類內部管理橫幅廣告的印象和點擊跟蹤。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">在播放期間某個時刻將播放的多個廣告提供統一視圖的類。 
    <pre>
      表示連續序列的廣告，這些廣告被剪接到內容中。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">表示與資產關聯的按一下實例的類。 此實例包含有關點擊式URL和標題的資訊，這些資訊可用於向用戶提供附加資訊。 
    <pre>
      表示與資產關聯的按一下實例。 此實例包含有關點擊式URL和標題的資訊，這些資訊可用於向用戶提供附加資訊。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定義AdPolicySelector API調用屬性的協定。 這些屬性提供了強制執行每個廣告行為的上下文。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> 一種用於強制廣告行為的廣告策略選擇器協定。 應用程式可以通過實施所有必需的方法或通過擴展現有預設策略選擇器類來自定義特定行為來遵循此協定。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAd時間軸</a></td> 
   <td colname="2"> 表示內容中斷時間線的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 類， 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 協定
    </pre> </td> 
   <td colname="2"> 處理Adobe Primetime廣告決策過程中廣告解析部分的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 描述自定義內容解析器( <span class="codeph"> PTContentResolver</span> )應用於與委派通信以解析內容的狀態。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacement類型</a> </td> 
   <td colname="2">抽取放置資訊請求的類。 每個已解析的廣告必須附加一個放置資訊。 該放置資訊描述了廣告要放置在時間軸上的位置。 它包含以下資訊： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">位置（毫秒） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">放置的類型（前滾、中滾或後滾） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">將要替換的主內容塊的持續時間 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
