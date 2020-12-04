---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 瀏覽器TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。
seo-description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 瀏覽器TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。
seo-title: ID3標籤
title: ID3標籤
uuid: a47cd0cc-b11d-47df-b1fb-56918896ef4c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# ID3標籤{#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案的標題或藝術家的姓名。 瀏覽器TVSDK會在HLS串流的傳輸串流(TS)區段層級偵測ID3標籤，並派單事件。 應用程式可從標籤擷取資料。

當在基礎HLS串流中找到新的ID3中繼資料時，瀏覽器TVSDK會觸發`AdobePSDK.TimedMetadataEvent`事件。

ID3的`TimedMetadata`物件具有下列屬性：

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性名稱 </th> 
   <th colname="col2" class="entry"> 詳細資訊 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span>物件類型。 </p> <p>對於ID3中繼資料，其值為<span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 時間  </span> </p> </td> 
   <td colname="col2"> <p> 偵測到此計時中繼資料的播放器時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span>物件的ID。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 名稱  </span> </p> </td> 
   <td colname="col2"> <p><span class="codeph"> TimedMetadata </span>物件的名稱。 對於ID3中繼資料，值為「ID3」。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 內容  </span> </p> </td> 
   <td colname="col2"> <p>計時中繼資料內容。 對於ID3標籤，此值代表序號位元組陣列。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 中繼資料  </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> 處理的資訊，此資訊是 <span class="codeph"> AdobePSDK的例項。儲 </span> 存ID3影格的中繼資料。 </p> <p> <p>注意： 對於Safari <span class="codeph">視訊</span>標籤，ID3標籤的特定影格資料會透過<span class="codeph"> AdobePSDK.Metadata </span>物件以物件形式公開，而對於其他瀏覽器，ID3標籤的影格資料則會透過<span class="codeph"> AdobePSDK.Metada5&gt;物件。</span> </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

應用程式可透過下列兩種方式擷取儲存在`TimedMetadata`中的各種ID3標籤：

* 在AdobePSDK.PSDKeventType.TIMED_METADATA_AVAILABLE事件偵聽器中。

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var mediaPlayer = new AdobePSDK.MediaPlayer(); 
   mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
       var td = event.timedMetadata; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   }); 
   ```

* 使用`MediaPlayerItem`的`timedMetadata`屬性。

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var timedMetadataList = player.currentItem.timedMetadata; 
   for(var i = 0; i < timedMetadataList.length; i++){ 
       var td = timedMetadataList[i]; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   } 
   ```

