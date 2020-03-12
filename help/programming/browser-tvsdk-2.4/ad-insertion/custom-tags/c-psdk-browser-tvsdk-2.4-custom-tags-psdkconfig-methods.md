---
description: 您可以使用MediaPlayerItemConfig類別，在串流中設定自訂標籤名稱。
seo-description: 您可以使用MediaPlayerItemConfig類別，在串流中設定自訂標籤名稱。
seo-title: 標籤的Config類方法
title: 標籤的Config類方法
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# 標籤的Config類方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig類別，在串流中設定自訂標籤名稱。

To create a new `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

以下是如何使用方法來管 `MediaPlayerItemConfig` 理自訂標籤的一些資訊：

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定的自訂標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>擷取目前訂閱標籤的清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>設定應用程式公開的訂閱標籤清單。 </p> <p>您的應用程式也會自動訂閱透過adTags傳輸的所有 <span class="codeph"> 標籤 </span>。 </p> </td> 
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
   <td colname="col2"> <p>擷取廣告標籤的目前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>設定預設業務機會生成器要使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住：

* 自訂標籤名稱必須包含首 `#` 碼。

   例如，是 `#EXT-X-ASSET` 正確的自訂標籤名稱，但 `EXT-X-ASSET` 不正確。

* 媒體串流載入後，您無法變更設定。

