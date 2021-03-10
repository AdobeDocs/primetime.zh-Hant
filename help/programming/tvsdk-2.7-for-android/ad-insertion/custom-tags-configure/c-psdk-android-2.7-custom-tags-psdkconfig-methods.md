---
description: 您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。
title: 標籤的Config類方法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 標籤{#config-class-methods-for-tags}的Config類方法

您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。

TVSDK會自動將全域組態套用至任何未指定串流特定組態的媒體串流。

`MediaPlayerItemConfig` 公開這些方法以管理自訂標籤：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定的自訂標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags  </span> </td> 
   <td colname="col2"> <p>擷取目前訂閱標籤的清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>設定將公開至應用程式的訂閱標籤清單。 </p> <p>您的應用程式也會自動訂閱透過<span class="codeph"> setAdTags </span>傳輸的所有標籤。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自訂預設機會偵測器使用的廣告標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags;  </span> </td> 
   <td colname="col2"> <p>擷取廣告標籤的目前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags);  </span> </td> 
   <td colname="col2"> <p>設定預設業務機會生成器將使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住：

* setter方法不允許標籤參數包含空值。

   如果遇到此問題，TVSDK會拋出`IllegalArgumentException`。
* 自訂標籤名稱必須包含`#`首碼。

   例如，`#EXT-X-ASSET`是正確的自訂標籤名稱，但`EXT-X-ASSET`不正確。

* 媒體串流載入後，您無法變更設定。
