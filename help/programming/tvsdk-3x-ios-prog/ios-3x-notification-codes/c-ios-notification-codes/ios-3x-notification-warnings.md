---
description: 此表格證明WARN型別通知的詳細資訊。
title: 警告通知代碼
exl-id: de922934-9775-463f-a28f-fc891d7a914b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 3%

---

# 警告通知代碼 {#warning-notification-codes}

此表格證明WARN型別通知的詳細資訊。

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

大多數警告包含相關的中繼資料，例如下載失敗的資源的URL。 某些通知包含中繼資料，用於指定問題發生在主要視訊內容、替代音訊內容還是廣告中。

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>程式碼</b></th> 
   <th colname="2" class="entry"><b>名稱</b></th> 
   <th colname="3" class="entry"><b>InnerNotification&gt;/b&gt;</th> 
   <th colname="4" class="entry"><b>中繼資料索引鍵</b></th> 
   <th colname="5" class="entry"><b>註解</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告解析</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_ FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET， INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>嘗試載入廣告創意時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_ RETURNED_NO_ADS</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR， AD_ID，說明</span> </td> 
   <td colname="5"> <p>廣告解析失敗，因為VAST URL無效，或因為VAST包裝函式未傳回任何廣告。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>背景資訊清單</b> </td> 
   <td colname="2"> </td>
   <td colname="3"> </td>
   <td colname="4"> </td>
   <td colname="5"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_警告</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span> <span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p> 背景資訊清單下載發生錯誤。 更新背景資訊清單的任何問題都會以TVSDK警告傳送，而不會導致播放停止。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_警告</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p></p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> 未定義_時間範圍 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 廣告訊號模式定義為自訂範圍，但沒有定義任何範圍。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_範圍 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p> 一個或多個時間範圍無效，將被忽略或修改。 </p> <p> DESCRIPTION是包含無效範圍說明的字串。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS特定</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_NOT_READY </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>未在資料流上插入AD。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_AUDIOONLY_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>廣告不包含純音訊資料流 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_MATCHING_BITRATE_MISSING </span> </td> 
   <td colname="3"><span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>找不到與內容目前位元速率相符的廣告資料流。 </p> <p>  </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270005 </span> </td> 
   <td colname="2"><span class="codeph"> AVASSET_FAILED_TO_CREATE </span> </td> 
   <td colname="3"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>建立AVAset時發生錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270006 </span> </td> 
   <td colname="2"><span class="codeph"> SiteCatalyst_警告 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>警告：請參閱sitecatalyst警告說明。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 270007 </span> </td> 
   <td colname="2"><span class="codeph"> NETWORK_ERROR </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>從網路取得資料時發生錯誤。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>adID和來源(URL)可透過通知中繼資料中的PTAdAsset擷取，並具有 `AD_ASSET` 金鑰。
>
>此 [] attribute會指定通知的選用索引鍵。
