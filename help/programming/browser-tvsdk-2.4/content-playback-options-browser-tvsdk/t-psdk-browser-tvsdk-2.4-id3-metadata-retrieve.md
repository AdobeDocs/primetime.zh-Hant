---
description: ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 瀏覽器TVSDK會在HLS資料流的傳輸資料流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。
title: ID3標籤
exl-id: 33510821-9de4-41fc-b404-bcf0b6ba86ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# ID3標籤{#id-tags}

ID3標籤提供音訊或視訊檔案的相關資訊，例如檔案標題或藝人姓名。 瀏覽器TVSDK會在HLS資料流的傳輸資料流(TS)區段層級偵測ID3標籤，並傳送事件。 應用程式可從標籤中擷取資料。

在基礎HLS資料流中找到新的ID3中繼資料時，瀏覽器TVSDK會觸發 `AdobePSDK.TimedMetadataEvent` 事件。

此 `TimedMetadata` ID3的物件具有下列屬性：

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性名稱 </th> 
   <th colname="col2" class="entry"> 詳細資料 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type </span> </p> </td> 
   <td colname="col2"> <p>一種型別 <span class="codeph"> TimedMetadata </span> 物件。 </p> <p>對於ID3中繼資料，值為 <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 時間 </span> </p> </td> 
   <td colname="col2"> <p> 偵測到此計時中繼資料的播放器時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID <span class="codeph"> TimedMetadata </span> 物件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 名稱 </span> </p> </td> 
   <td colname="col2"> <p>名稱： <span class="codeph"> TimedMetadata </span> 物件。 若為ID3中繼資料，值為「ID3」。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 內容 </span> </p> </td> 
   <td colname="col2"> <p>定時中繼資料內容。 對於ID3標籤，此值代表序列化的位元組陣列。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 中繼資料 </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> 已處理的資訊，此資訊是 <span class="codeph"> AdobePSDK.Metadata </span> 儲存ID3影格的位置。 </p> <p> <p>注意：適用於Safari <span class="codeph"> 視訊 </span> 標籤，ID3標籤的特定框架資料會透過 <span class="codeph"> AdobePSDK.Metadata </span> 物件，而對於其他瀏覽器，ID3標籤的框架資料會透過以位元組陣列的形式公開 <span class="codeph"> AdobePSDK.Metadata </span> 物件。 </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

儲存於中的各種ID3標籤 `TimedMetadata` 應用程式可透過下列兩種方式來擷取：

* 在AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE事件監聽器中。

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

* 使用 `MediaPlayerItem`的 `timedMetadata` 屬性。

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
