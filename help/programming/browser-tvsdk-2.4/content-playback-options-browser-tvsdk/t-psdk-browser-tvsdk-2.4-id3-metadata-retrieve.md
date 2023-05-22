---
description: ID3標籤提供有關音頻或視頻檔案的資訊，如檔案的標題或藝術家的姓名。 瀏覽器TVSDK檢測HLS流中傳輸流(TS)段級別的ID3標籤並調度事件。 應用程式可以從標籤中提取資料。
title: ID3標籤
exl-id: 33510821-9de4-41fc-b404-bcf0b6ba86ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# ID3標籤{#id-tags}

ID3標籤提供有關音頻或視頻檔案的資訊，如檔案的標題或藝術家的姓名。 瀏覽器TVSDK檢測HLS流中傳輸流(TS)段級別的ID3標籤並調度事件。 應用程式可以從標籤中提取資料。

當在基礎HLS流中找到新的ID3元資料時，瀏覽器TVSDK將觸發 `AdobePSDK.TimedMetadataEvent` 的子菜單。

的 `TimedMetadata` ID3的對象具有以下屬性：

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性名稱 </th> 
   <th colname="col2" class="entry"> 詳細資訊 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 類型 </span> </p> </td> 
   <td colname="col2"> <p>類型 <span class="codeph"> TimedMetadata </span> 的雙曲餘切值。 </p> <p>對於ID3元資料，值為 <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 時間 </span> </p> </td> 
   <td colname="col2"> <p> 檢測到此定時元資料的播放器時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> ID </span> </p> </td> 
   <td colname="col2"> <p>ID <span class="codeph"> TimedMetadata </span> 的雙曲餘切值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 名稱 </span> </p> </td> 
   <td colname="col2"> <p>名稱 <span class="codeph"> TimedMetadata </span> 的雙曲餘切值。 對於ID3元資料，值為「ID3」。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 內容 </span> </p> </td> 
   <td colname="col2"> <p>定時元資料內容。 對於ID3標籤，此值表示序列化的位元組陣列。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> 元資料 </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> 已處理資訊，即 <span class="codeph"> AdobePSDK.元資料 </span> 儲存ID3幀的位置。 </p> <p> <p>注：對於Safari <span class="codeph"> 視頻 </span> 標籤，ID3標籤的特定幀資料以對象形式通過 <span class="codeph"> AdobePSDK.元資料 </span> 對象，而對於其他瀏覽器，ID3標籤的幀資料以位元組陣列的形式通過 <span class="codeph"> AdobePSDK.元資料 </span> 的雙曲餘切值。 </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

儲存在 `TimedMetadata` 可通過以下兩種方式檢索：

* 在AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE事件偵聽器中。

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

* 使用 `MediaPlayerItem``s `timedMetadata` 屬性。

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
