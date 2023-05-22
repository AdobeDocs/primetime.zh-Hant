---
title: NATIVE_ERROR通知的詳細資訊
description: NATIVE_ERROR通知的詳細資訊
copied-description: true
exl-id: 2b75d1ef-bfac-4e2e-a2e8-ee40b25eb8b3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# NATIVE_ERROR通知的詳細資訊 {#details-for-the-native-error-notification}

當TVSDK處理本機錯誤時，它會設定以下部分或全部元資料鍵值。

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 元資料密鑰名稱 </th> 
   <th colname="col2" class="entry"> 元資料值 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 運行時代碼 </span> </td> 
   <td colname="col2"> 
    <pre>
      來自Flash Player的本機錯誤代碼。 
    </pre> 這些代碼表示以下內容： 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM錯誤（代碼3300到3367）。 這些與等效Flash Player錯誤代碼相同。 </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">視頻播放錯誤（–1到89）。 </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">密碼錯誤（300到307）。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 運行時代碼消息 </span> </td> 
   <td colname="col2"> 包含錯誤名稱的字串；比如說， <span class="codeph"> AAXS_InvalidVoucher </span> 或 <span class="codeph"> 解碼器失敗 </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 運行時_子錯誤_代碼 </span> </td> 
   <td colname="col2"> 對於DRM錯誤，還返回子錯誤代碼。 這些代碼與 <span class="codeph"> DRMError事件 </span> Flash Player返回的子錯誤代碼。 將錯誤報告給Adobe時，請包括此數字值以用於故障排除幫助。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> 對於DRM，這是DRM伺服器部署中的自定義錯誤字串（如果定義了）。 在向Adobe報告錯誤時，還應包括此內容。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 說明 </span> </td> 
   <td colname="col2"> 錯誤的字串描述。 通常是媒體的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 資源URL </span> </td> 
   <td colname="col2"> 媒體的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 資源類型 </span> </td> 
   <td colname="col2"> 媒體類型(HLS)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 資源ID </span> </td> 
   <td colname="col2"> 媒體ID。 </td> 
  </tr> 
 </tbody> 
</table>

TVSDK從視頻引擎接收這些錯誤代碼和字串。

>[!IMPORTANT]
>
>有關Adobe PrimetimeDRM客戶端錯誤代碼的完整清單，請參見 [DRM客戶端錯誤消息參考](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf)。
