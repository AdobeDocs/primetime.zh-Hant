---
description: 可以使用MediaPlayerItemConfig類在流中配置自定義標籤名稱。
title: 標籤的Config類方法
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 標籤的Config類方法{#config-class-methods-for-tags}

可以使用MediaPlayerItemConfig類在流中配置自定義標籤名稱。

建立新 `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

下面是一些關於 `MediaPlayerItemConfig` 方法用於管理自定義標籤：

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>訂閱特定自定義標籤</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>檢索當前訂閱標籤清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>設定應用程式所暴露的訂閱標籤清單。 </p> <p>您的應用程式還會自動訂閱通過傳輸的所有標籤 <span class="codeph"> adTags </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定義預設機會檢測器使用的廣告標籤 </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>檢索廣告標籤的當前清單。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>設定預設機會生成器要使用的廣告標籤清單。 </p> </td> 
  </tr> 
 </tbody> 
</table>

請記住以下內容：

* 自定義標籤名稱必須包含 `#` 前置詞。

   比如說， `#EXT-X-ASSET` 是正確的自定義標籤名稱，但 `EXT-X-ASSET` 不正確。

* 在載入媒體流後，不能更改配置。
