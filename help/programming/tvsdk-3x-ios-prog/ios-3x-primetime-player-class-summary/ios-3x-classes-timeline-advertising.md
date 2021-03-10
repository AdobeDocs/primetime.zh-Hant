---
description: 這些類別提供有關時間軸中發生廣告的資訊。
title: 時間軸廣告課程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 時間軸廣告類{#timeline-advertising-classes}

這些類別提供有關時間軸中發生廣告的資訊。

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
   <td colname="2">定義廣告抽象並包含所有廣告資訊的類別。 它由唯一ID、持續時間和MediaResources定義。 MediaResource包含實際廣告內容所在的URL。 
    <pre>
      代表插入內容的主要線性資產。 它可以選擇性地包含必須與線性資產一起顯示的配套資產陣列。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">表示要顯示的資產的分類。 
    <pre>
      表示要顯示的資產。
    </pre> 
    <pre>
      代表廣告資產的分類。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      顯示橫幅資產。 您的應用程式必須建立此實用程式類的新實例、設定橫幅資產並將其添加到視圖中。 橫幅的曝光和點按追蹤由此類別內部管理。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">提供數個廣告統一檢視的類別，在播放期間的某個時間點播放。 
    <pre>
      代表連續的廣告序列，這些廣告會拼接至內容中。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">表示與資產關聯之點按例項的分類。 此例項包含有關點進URL和標題的資訊，這些資訊可用來提供使用者其他資訊。 
    <pre>
      代表與資產相關聯的點按例項。 此例項包含有關點進URL和標題的資訊，這些資訊可用來提供使用者其他資訊。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定義AdPolicySelector API呼叫屬性的通訊協定。 這些屬性提供實施每個廣告行為的上下文。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> 用於強制廣告行為的廣告策略選擇器協定。 應用程式可實作所有必要方法，或擴充現有的預設原則選擇器類別以自訂特定行為，以符合此通訊協定。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> 代表內容中斷時間軸的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverclass、 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> </a> PTContentResolverprotocol
    </pre> </td> 
   <td colname="2"> 在Adobe Primetime廣告決策程式中處理廣告解析部分的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 描述自定義內容解析器(<span class="codeph"> PTContentResolver</span>)用於向委派通信內容解析狀態的方法的協定。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">抽象位置資訊要求的類別。 每個已解決的廣告都必須附上一個位置資訊。 位置資訊說明廣告要放置在時間軸上的位置。 它包含以下資訊： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">位置（毫秒） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">位置類型（前滾、中滾或後滾） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">將要替換的主要內容塊的持續時間 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>