---
description: 可以使用MediaPlayerItemConfig類全局配置TVSDK中的自定義標籤名稱，或使用MediaPlayerItemConfig類基於流。
title: 標籤的Config類方法
exl-id: 093720df-9c2d-41f1-ba9d-9553c5df40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 標籤的Config類方法{#config-class-methods-for-tags}

可以使用MediaPlayerItemConfig類全局配置TVSDK中的自定義標籤名稱，或使用MediaPlayerItemConfig類基於流。

TVSDK自動將全局配置應用於未指定流特定配置的任何媒體流。

兩者 `PSDKConfig` 和 `MediaPlayerItemConfig` 公開這些方法以管理自定義標籤：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>訂閱特定自定義標籤</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式get subscribeTags():Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 檢索當前訂閱標籤清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函式set subscribeTags():Vector。&lt;String&gt;</span> </td> 
   <td colname="col2">設定將公開給應用程式的訂閱標籤清單。 <p>您的應用程式還自動訂閱通過傳輸的所有標籤 <span class="codeph"> adTags</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自定義預設機會檢測器使用的廣告標籤 </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式get adTags():Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 檢索廣告標籤的當前清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函式set adTags():Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 設定預設機會生成器將使用的廣告標籤清單。 </td> 
  </tr> 
 </tbody> 
</table>

請記住以下內容：

* setter方法不允許標籤參數包含空值。

   如果遇到，TVSDK將引發 `IllegalArgumentException`。
* 自定義標籤名稱必須包含#前置詞。

   比如說， `#EXT-X-ASSET` 是正確的自定義標籤名稱，但 `EXT-X-ASSET` 不正確。
* 在載入媒體流後，不能更改配置。
