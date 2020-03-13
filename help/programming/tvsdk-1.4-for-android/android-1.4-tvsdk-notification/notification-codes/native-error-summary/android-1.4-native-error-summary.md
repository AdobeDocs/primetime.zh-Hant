---
seo-title: NATIVE_ERROR通知的詳細資訊
title: NATIVE_ERROR通知的詳細資訊
uuid: 18c4da57-59de-41a8-a2ea-fef800565207
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# NATIVE_ERROR通知的詳細資訊 {#details-for-the-native-error-notification}

當TVSDK處理原生錯誤時，會設定下列部分或全部中繼資料索引鍵值。

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 中繼資料索引鍵名稱 </th> 
   <th colname="col2" class="entry"> 中繼資料值 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <ph>
      AVE中的原生錯誤代碼。 
    </ph> 這些代碼代表下列： 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM錯誤（代碼3300到3367）。 這些錯誤碼與相當的Flash Player錯誤碼相同。 </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">視訊播放錯誤（-1到89）。 </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">加密錯誤（300到307）。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> 包含錯誤名稱的字串；例如， <span class="codeph"> AAXS_InvalidVoucher </span> 或 <span class="codeph"> DECODER_FAILED </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> 對於DRM錯誤，也會傳回子錯誤碼。 這些代碼對應 <span class="codeph"> 於Flash Player傳 </span> 回的DRMErrorEvents子錯誤代碼。 向Adobe報告錯誤時，請加入此數值以取得疑難排解協助。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> 對於DRM，這是您在DRM伺服器部署（如果已定義）中自定義的錯誤字串。 在向Adobe報告錯誤時也加入此功能。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 說明 </span> </td> 
   <td colname="col2"> 錯誤的字串說明。 通常是媒體的URL。 </td> 
  </tr> 
 </tbody> 
</table>

TVSDK會從視訊引擎接收這些錯誤碼和字串。

>[!IMPORTANT]
>
>如需Adobe Primetime DRM用戶端錯誤碼的完整清單，請參閱 [DRM用戶端錯誤訊息參考](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf)。