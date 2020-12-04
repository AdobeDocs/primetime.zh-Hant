---
description: 您可以使用MediaPlayerItemConfig類別，或使用MediaPlayerItemConfig類別，在TVSDK中設定自訂標籤名稱，以串流為基礎。
seo-description: 您可以使用MediaPlayerItemConfig類別，或使用MediaPlayerItemConfig類別，在TVSDK中設定自訂標籤名稱，以串流為基礎。
seo-title: 標籤的Config類方法
title: 標籤的Config類方法
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 標籤的Config類方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別，或使用MediaPlayerItemConfig類別，在TVSDK中設定自訂標籤名稱，以串流為基礎。

TVSDK會自動將全域組態套用至任何未指定串流特定組態的媒體串流。

`PSDKConfig`和`MediaPlayerItemConfig`都會公開這些方法來管理自訂標籤：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>訂閱特定的自訂標籤</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式get subscribeTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 擷取目前訂閱標籤的清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式集subscribeTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2">設定將公開至應用程式的訂閱標籤清單。 <p>您的應用程式也會自動訂閱透過<span class="codeph"> adTags</span>傳輸的所有標籤。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自訂預設機會偵測器使用的廣告標籤  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式get adTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 擷取廣告標籤的目前清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式set adTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 設定預設業務機會生成器將使用的廣告標籤清單。 </td> 
  </tr> 
 </tbody> 
</table>

請記住：

* setter方法不允許標籤參數包含空值。

   如果遇到此問題，TVSDK會拋出`IllegalArgumentException`。
* 自訂標籤名稱必須包含#首碼。

   例如，`#EXT-X-ASSET`是正確的自訂標籤名稱，但`EXT-X-ASSET`不正確。
* 媒體串流載入後，您無法變更設定。

