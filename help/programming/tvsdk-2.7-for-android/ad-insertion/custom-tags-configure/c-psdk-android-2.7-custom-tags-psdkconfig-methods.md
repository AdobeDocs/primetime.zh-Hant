---
description: 您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-description: 您可以使用MediaPlayerItemConfig類別，在TVSDK中全域設定自訂標籤名稱。
seo-title: 標籤的Config類方法
title: 標籤的Config類方法
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 標籤的Config類方法 {#config-class-methods-for-tags}

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
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>擷取目前訂閱標籤的清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>設定將公開至應用程式的訂閱標籤清單。 </p> <p>您的應用程式也會自動訂閱透過setAdTags傳輸的所 <span class="codeph"> 有標籤 </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自訂預設機會偵測器使用的廣告標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>擷取廣告標籤的目前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>設定預設業務機會生成器將使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住：

* setter方法不允許標籤參數包含空值。

   如果遇到此問題，TVSDK會拋出 `IllegalArgumentException`。
* 自訂標籤名稱必須包含首 `#` 碼。

   例如，是 `#EXT-X-ASSET` 正確的自訂標籤名稱，但 `EXT-X-ASSET` 不正確。

* 媒體串流載入後，您無法變更設定。
