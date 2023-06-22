---
description: 您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱，或使用MediaPlayerItemConfig類別以資料流為基礎。
title: 標籤的設定類別方法
exl-id: 093720df-9c2d-41f1-ba9d-9553c5df40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 標籤的設定類別方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱，或使用MediaPlayerItemConfig類別以資料流為基礎。

TVSDK會自動將全域設定套用至未指定資料流特定設定的任何媒體資料流。

兩者 `PSDKConfig` 和 `MediaPlayerItemConfig` 公開這些方法來管理自訂標籤：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>訂閱特定自訂標籤</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公用函式取得subscribeTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 擷取訂閱標籤的目前清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公用函式集subscribeTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2">設定將公開給應用程式的訂閱標籤清單。 <p>您的應用程式也會自動訂閱透過傳輸的所有標籤 <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自訂預設機會偵測器使用的廣告標籤 </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式get adTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 擷取目前的廣告標籤清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公用函式set adTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 設定預設機會產生器將使用的廣告標籤清單。 </td> 
  </tr> 
 </tbody> 
</table>

請記住以下事項：

* setter方法不允許tags引數包含null值。

   如果發生，TVSDK會擲回 `IllegalArgumentException`.
* 自訂標籤名稱必須包含#首碼。

   例如， `#EXT-X-ASSET` 是正確的自訂標籤名稱，但 `EXT-X-ASSET` 不正確。
* 媒體資料流載入後，您就無法變更設定。
