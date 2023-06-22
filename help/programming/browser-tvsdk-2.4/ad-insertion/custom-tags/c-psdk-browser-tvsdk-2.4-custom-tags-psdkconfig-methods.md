---
description: 您可以使用MediaPlayerItemConfig類別在資料流中設定自訂標籤名稱。
title: 標籤的設定類別方法
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 標籤的設定類別方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別在資料流中設定自訂標籤名稱。

若要建立新的 `MediaPlayerItemConfig`：

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

以下提供一些關於如何 `MediaPlayerItemConfig` 管理自訂標籤的方法如下：

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定自訂標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>擷取訂閱標籤的目前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>設定向應用程式公開的訂閱標籤清單。 </p> <p>您的應用程式也會自動訂閱所有透過傳輸的標籤 <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自訂預設機會偵測器使用的廣告標籤 </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>擷取目前的廣告標籤清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>設定預設機會產生器使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住以下事項：

* 自訂標籤名稱必須包含 `#` 前置詞。

   例如， `#EXT-X-ASSET` 是正確的自訂標籤名稱，但 `EXT-X-ASSET` 不正確。

* 媒體資料流載入後，您就無法變更設定。
