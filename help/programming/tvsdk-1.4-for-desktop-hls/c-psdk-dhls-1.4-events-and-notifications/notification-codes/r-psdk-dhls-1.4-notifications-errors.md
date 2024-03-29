---
description: 此表格提供有關ERROR型別通知的詳細資訊。
title: 錯誤通知代碼
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# 錯誤通知代碼{#error-notification-codes}

此表格提供有關ERROR型別通知的詳細資訊。

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

大多數錯誤包含相關的中繼資料，例如無法下載的資源的URL。 有些通知包含中繼資料，用於指定問題發生在主要視訊內容、替代音訊內容還是廣告中。

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 程式碼 </th> 
   <th colname="2" class="entry"> 名稱 </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> 中繼資料索引鍵 </th> 
   <th colname="5" class="entry"> 註解 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> 主要DRM代碼 </span><span class="codeph"> 次要_DRM_CODE </span><span class="codeph"> 說明 </span> </td> 
   <td colname="5">另請參閱106000 (
     <span class="codeph"> NATIVE_ERROR</span>)。
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>下載片段或區段（視訊和音訊）時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101006 </span> </td> 
   <td colname="2"><span class="codeph"> 安全性_錯誤 </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008</span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>執行暫停作業時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> <p>執行搜尋作業時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>擷取有關內容時段的資訊時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>嘗試擷取播放位置時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>嘗試擷取QOS資訊時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>嘗試下載資料時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>無效的資源 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> 資源 </span> </td> 
   <td colname="5"> <p>載入資源專案時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_失敗 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> <p>將資源放在播放時間表上時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告處理 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 無 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_無效 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>由於廣告中繼資料格式無效，廣告解析失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_失敗 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> <p>廣告外掛程式無法解析廣告。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3">無</td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> <p>廣告解析階段已失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>原生</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> RUNTIME_CODE</span> <span class="codeph"> RUNTIME_CODE_MESSAGE</span> <span class="codeph"> RESOURCE_URL</span> <span class="codeph"> 資源型別</span> <span class="codeph"> RESOURCE_ID</span> <p><b>DRM詳細資料：</b> </p> <span class="codeph"> drm_ERROR_STRING</span> <span class="codeph"> RUNTIME_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>低階AVE程式庫發生錯誤。 </p> <p>另請參閱 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的詳細資料</a> 這些中繼資料索引鍵值的相關資訊。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>具現化AVE低階程式庫時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>發行AVE低階程式庫時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>釋放AVE程式庫所使用的GPU資源時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>重設AVE程式庫時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_檢視錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>將檢視附加至AVE程式庫時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>替代音訊</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> 音訊曲目名稱 </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> <p>發生與音軌相關的錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>標籤一般錯誤事件。 並非由TVSDK實際發行。 它只是對應至TVSDK錯誤事件的數值代碼範圍結尾的標籤。 </p> </td> 
  </tr> 
 </tbody> 
</table>
