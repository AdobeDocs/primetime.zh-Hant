---
description: 這些類別會提供發生在時間軸內之廣告的相關資訊。
title: 時間表廣告類別
exl-id: 004c706a-55cc-446a-93b1-c5c7c011ba42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 時間表廣告類別{#timeline-advertising-classes}

這些類別會提供發生在時間軸內之廣告的相關資訊。

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名稱 </th> 
   <th colname="2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">定義廣告抽象並保留所有廣告資訊的類別。 它由唯一ID、持續時間和MediaResource定義。 MediaResource包含實際廣告內容所在的URL。 
    <pre>
      代表連結至內容的主要線性資產。 它可選擇包含一系列必須隨線性資產一起顯示的隨附資產。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">代表要顯示之資產的類別。 
    <pre>
      代表要顯示的資產。
    </pre> 
    <pre>
      代表廣告資產的類別。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      顯示橫幅資產。 您的應用程式必須建立此公用程式類別的新執行個體、設定橫幅資產，並將其新增至檢視。 橫幅的曝光和點選追蹤功能是由此類別內部管理。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">在播放期間某個時間點播放的數個廣告上提供統一檢視的類別。 
    <pre>
      代表插入內容中的連續廣告順序。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">代表與資產相關聯之點選例項的類別。 此執行個體包含點進URL和標題的相關資訊，可用於向使用者提供其他資訊。 
    <pre>
      代表與資產相關聯的點選執行個體。 此執行個體包含點進URL和標題的相關資訊，可用於向使用者提供其他資訊。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定義AdPolicySelector API呼叫屬性的通訊協定。 這些屬性提供強制實行每個廣告行為的內容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ptadPolicySelector</td> 
   <td colname="2"> 用於強制實施廣告行為的廣告原則選擇器通訊協定。 應用程式可以透過實作所有必要的方法或擴充現有的預設原則選擇器類別來自訂特定行為，來符合此通訊協定。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAd時間軸</td> 
   <td colname="2"> 代表內容中分行時間軸的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 類別， 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 通訊協定
    </pre> </td> 
   <td colname="2"> 在Adobe Primetime廣告決策程式中處理廣告解析部分的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 說明自訂內容解析器( <span class="codeph"> PTContentResolver</span> )應該使用向委派通訊內容解析的狀態。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">抽象位置資訊請求的類別。 每個已解析廣告都必須附加一個版位資訊。 位置資訊說明廣告在時間軸上的放置位置。 其中包含下列資訊： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">位置位置（以毫秒為單位） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">位置型別（前段、中段或後段） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">即將取代之主要內容區塊的持續時間 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
