---
description: 此表證明了有關WARN類型通知的詳細資訊。
title: 警告通知代碼
exl-id: e787fad5-fbdc-416d-b03d-8c84f4884c5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# 警告通知代碼 {#warning-notification-codes}

此表證明了有關WARN類型通知的詳細資訊。

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

大多數警告都包含相關的元資料，例如，無法下載的資源的URL。 某些通知包含元資料，用於指定是在主視頻內容、備用音頻內容還是廣告中出現問題。

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 代碼 </th> 
   <th colname="2" class="entry"> 名稱 </th> 
   <th colname="3" class="entry"> 內部通知 </th> 
   <th colname="4" class="entry"> 元資料鍵 </th> 
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
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> 回放操作失敗(_F) </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> 查找錯誤 </span> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>與回放相關的操作失敗，但回放可能會繼續。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告解析</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_失敗 </span><span class="codeph"> AD_RESOLVER_METADATA_INVALID </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>ad解析程式無法解析/插入廣告內容。 播放可能會繼續。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET,INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>嘗試載入廣告創意時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR,AD_ID,DESCRIPTION</span> </td> 
   <td colname="5"> <p>由於無效的VAST URL或未從VAST包裝返回任何廣告，廣告解析失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>背景清單</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_警告</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_警告_錯誤</span> <span class="codeph"> BACKGROUND_MANIFEST_警告_名稱</span> <span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p> 後台清單下載時出錯。 更新後台清單中的任何問題都會作為TVSDK警告發出，不會導致播放停止。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_警告</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>本機</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> 本機警告 </span> </td> 
   <td colname="3" morerows="1"> <p>無 </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> 本機錯誤代碼 </span><span class="codeph"> 本機錯誤名稱 </span><span class="codeph"> 說明 </span> </p> </td> 
   <td colname="5"> <p>低級AVE庫發出錯誤。 </p> <p>請參閱 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的詳細資訊</a> 的子菜單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> DRM次錯誤代碼和DRM伺服器錯誤字串。 請參閱 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的詳細資訊</a> 的子菜單。</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>時間範圍集合</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> 未定義的_時間範圍 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 廣告信令模式被定義為自定義範圍，但沒有定義任何範圍。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_範圍 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p> 一個或多個時間範圍無效，將忽略或修改。 </p> <p> DESCRIPTION是包含無效範圍描述的字串。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>特技模式</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000 </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_CHANGE_FAIL</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p> 匯率更改失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>泛型</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> 泛型警告 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>標籤泛型警告事件。 不是TVSDK發的。 它只是一個標籤，表示與警告事件相對應的數字代碼範圍的結束。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[注意！] 可以通過PTAdAsset在通知元資料中檢索到adID和源(URL) `AD_ASSET` 按鈕
