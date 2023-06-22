---
description: 您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱。
title: 標籤的設定類別方法
exl-id: 6b3e344f-1d50-4743-9cc4-bd0bc82a0b9c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 標籤的設定類別方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域設定套用至未指定資料流特定設定的任何媒體資料流。

`MediaPlayerItemConfig` 公開這些方法來管理自訂標籤：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定自訂標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags() </span> </td> 
   <td colname="col2"> 擷取訂閱標籤的目前清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公開最終void setSubscribedTags（String[]標籤）； </span> </td> 
   <td colname="col2"> 設定將公開給應用程式的訂閱標籤清單。 <p>您的應用程式也會自動訂閱透過傳輸的所有標籤 <span class="codeph"> setadtags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自訂預設機會偵測器使用的廣告標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公用最終字串[] getAdTags()； </span> </td> 
   <td colname="col2"> 擷取目前的廣告標籤清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公開最終void setAdTags（String[]標籤）； </span> </td> 
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
