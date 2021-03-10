---
description: 此表提供了有關ERROR類型通知的詳細資訊。
title: 錯誤通知代碼
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 4%

---


# 錯誤通知代碼{#error-notification-codes}

此表提供了有關ERROR類型通知的詳細資訊。

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

大部分錯誤都包含相關的中繼資料，例如無法下載的資源URL。 有些通知包含中繼資料，以指定問題是發生在主要視訊內容、替代音訊內容或廣告中。

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 程式碼 </th> 
   <th colname="2" class="entry"> 名稱 </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> 中繼資料索引鍵 </th> 
   <th colname="5" class="entry"> 注釋 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000  </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號101004  </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> 下載片段或區段（視訊和音訊）時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號101008  </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span><span class="codeph"> DESIRED_SEEK_POSITION  </span><span class="codeph"> DESIRED_SEEK_PERIOD  </span> </td> 
   <td colname="5"> 執行尋道操作時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號101009  </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> 執行暫停操作時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：101102  </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 擷取內容時段的相關資訊時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：101103  </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 嘗試擷取播放位置時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：101104  </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 嘗試檢索QOS資訊時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：101200  </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> URL  </span> </td> 
   <td colname="5"> 嘗試下載資料時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>資源無效</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：102100  </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明資 </span><span class="codeph"> 源  </span> </td> 
   <td colname="5"> 載入資源項時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：102101  </span> </td> 
   <td colname="2"><span class="codeph"> 資源放置失敗  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID  </span> </td> 
   <td colname="5"> 在播放時間軸上放置資源時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告處理</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編104000  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL  </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA _INVALID  </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL  </span><span class="codeph"> AD_RESOLVE_FAIL  </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE  </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 無 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號104001  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_無效  </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> 由於無效的廣告中繼資料格式，廣告解析失敗。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號104003  </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVE_FAIL  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE  </span> </td> 
   <td colname="5"> 廣告外掛程式無法解析廣告。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號104005  </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> PRESITED_AD_BREAK</span> </td> 
   <td colname="5"> 廣告解析階段失敗。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>原生</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編106000  </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE  </span> <span class="codeph"> NATIVE_ERROR_NAME說明 </span> <span class="codeph"> 說 </span> <span class="codeph"> 明</span> <p><b>DRM詳細資訊：</b> </p> <span class="codeph"> DRM_ERROR_</span> <span class="codeph"> STRINGNATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>低級AVE庫發出錯誤。 </p> <p>有關這些元資料鍵值的資訊，請參閱NATIVE_ERROR通知</a>的<a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external">詳細資訊。 </a></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號106001  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 實例化AVE低級庫時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號106002  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_錯誤  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 釋放AVE低級庫時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號106003  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 釋放AVE庫使用的GPU資源時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號106004  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 重設AVE庫時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號106005  </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> 將視圖附加到AVE庫時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>配置</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：107000  </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明卷  </span> </td> 
   <td colname="5"> 嘗試設定卷級別時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號107001  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_錯誤  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> 嘗試更改緩衝參數時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號107002  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_錯誤  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> 嘗試變更CC音軌的可見度時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號107003  </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> 嘗試變更CC音軌的樣式選項時發生錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號107004  </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明  </span> </td> 
   <td colname="5"> 嘗試更改ABR控制參數時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵遞區號107005  </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR  </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> INITIAL_BUFFER_TIME  </span><span class="codeph"> PLAY_BUFFER_TIME  </span> </td> 
   <td colname="5"> 嘗試更改緩衝控制參數時出錯。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>替代音訊</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 郵編：109000  </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR  </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR  </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME  </span><span class="codeph"> AUDIO_TRACK_LANGUAGE  </span> </td> 
   <td colname="5"> 發生與音軌相關的錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 郵編：199999  </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 標籤一般錯誤事件。 並非由TVSDK實際核發。 這只是對應於TVSDK錯誤事件的數值代碼範圍結尾的標籤。 </td> 
  </tr> 
 </tbody> 
</table>

