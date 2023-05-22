---
description: 可以使用MediaPlayerItemConfig類在TVSDK中全局配置自定義標籤名稱。
title: 標籤的Config類方法
exl-id: 48e88284-788c-49b3-a370-3e3d77a8da6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 標籤的Config類方法 {#config-class-methods-for-tags}

可以使用MediaPlayerItemConfig類在TVSDK中全局配置自定義標籤名稱。

TVSDK自動將全局配置應用於未指定流特定配置的任何媒體流。

`MediaPlayerItemConfig` 公開了以下用於管理自定義標籤的方法：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定自定義標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公共最終字串[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>檢索當前訂閱標籤清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags（String[]標籤）; </span> </td> 
   <td colname="col2"> <p>設定將公開給應用程式的訂閱標籤清單。 </p> <p>您的應用程式還自動訂閱通過傳輸的所有標籤 <span class="codeph"> setAdTags </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定義預設機會檢測器使用的廣告標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公共最終字串[] getAdTags; </span> </td> 
   <td colname="col2"> <p>檢索廣告標籤的當前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags（String[]標籤）; </span> </td> 
   <td colname="col2"> <p>設定預設機會生成器將使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住以下內容：

* setter方法不允許標籤參數包含空值。

   如果遇到，TVSDK將引發 `IllegalArgumentException`。
* 自定義標籤名稱必須包含 `#` 前置詞。

   比如說， `#EXT-X-ASSET` 是正確的自定義標籤名稱，但 `EXT-X-ASSET` 不正確。

* 在載入媒體流後，不能更改配置。
