---
title: NATIVE_ERROR通知的詳細資料
description: NATIVE_ERROR通知的詳細資料
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# NATIVE_ERROR通知的詳細資料 {#details-for-the-native-error-notification}

TVSDK處理原生錯誤時，會設定下列部分或全部中繼資料索引鍵值。

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 中繼資料金鑰名稱 </th> 
   <th colname="col2" class="entry"> 中繼資料值 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      來自AVE的原生錯誤代碼。 
    </pre> 這些程式碼代表下列專案： 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM錯誤（代碼3300至3367）。 這些與同等的Flash Player錯誤碼相同。 </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">視訊播放錯誤（–1到89）。 </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">加密錯誤（300到307）。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 原生錯誤名稱 </span> </td> 
   <td colname="col2"> 包含錯誤名稱的字串；例如， <span class="codeph"> AAXS_InvalidVoucher </span> 或 <span class="codeph"> 解碼器失敗 </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> 對於DRM錯誤，也會傳回子錯誤代碼。 這些程式碼對應至 <span class="codeph"> DRMErrorEvents </span> Flash Player傳回的子錯誤碼。 向Adobe報告錯誤時，請包含此數值以獲得疑難排解協助。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> drm_ERROR_STRING </span> </td> 
   <td colname="col2"> 對於DRM，這是您的DRM伺服器部署中的自訂錯誤字串（如果定義了任何字串）。 向Adobe報告錯誤時也包含此內容。 </td> 
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
>如需Adobe Primetime DRM使用者端錯誤碼的完整清單，請參閱 [DRM使用者端錯誤訊息參考](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).
