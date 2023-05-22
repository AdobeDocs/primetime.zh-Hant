---
description: 此表提供了有關ERROR類型通知的詳細資訊。
title: 錯誤通知代碼
exl-id: 4f8882b5-2c2b-4f17-a9c9-834816265e1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# 錯誤通知代碼{#error-notification-codes}

此表提供了有關ERROR類型通知的詳細資訊。

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

大多數錯誤都包含相關的元資料，例如，無法下載的資源的URL。 某些通知包含元資料，用於指定是在主視頻內容、備用音頻內容還是廣告中出現問題。

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_錯誤 </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> 次要_DRM_代碼 </span><span class="codeph"> 說明 </span> </td> 
   <td colname="5">另請參閱106000(
     <span class="codeph"> 本機錯誤</span>)。
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
   <td colname="2"><span class="codeph"> 回放錯誤 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> 內容錯誤 </span> </td> 
   <td colname="3"><span class="codeph"> 下載錯誤 </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>下載片段或段（視頻和音頻）時出錯。 </p> </td> 
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
   <td colname="2"><span class="codeph"> 暫停_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>執行暫停操作時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> 查找錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 本機錯誤代碼 </span><span class="codeph"> 所需_尋道_位置 </span><span class="codeph"> 所需_尋道_週期 </span> </td> 
   <td colname="5"> <p>執行查找操作時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>檢索有關內容期間的資訊時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> 檢索時間錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>嘗試檢索回放位置時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>嘗試檢索QOS資訊時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> 下載錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>嘗試下載資料時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>資源無效 </b> </td> 
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
   <td colname="5"> <p>載入資源項時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_失敗 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 內容ID </span> </td> 
   <td colname="5"> <p>將資源放在播放時間線上時出錯。 </p> </td> 
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
   <td colname="3"><span class="codeph"> AD_METADATA無效(_I) </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 無 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_無效 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>由於無效的ad-metadata格式，廣告解析失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_失敗 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 本機錯誤代碼 </span> </td> 
   <td colname="5"> <p>廣告插件無法解析廣告。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3">無</td> 
   <td colname="4"><span class="codeph"> 建議的_AD_BREAK</span> </td> 
   <td colname="5"> <p>廣告解析階段失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>本機</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> 本機錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 運行時代碼</span> <span class="codeph"> 運行時代碼消息</span> <span class="codeph"> 資源URL</span> <span class="codeph"> 資源類型</span> <span class="codeph"> 資源ID</span> <p><b>DRM詳細資訊：</b> </p> <span class="codeph"> DRM_ERROR_STRING</span> <span class="codeph"> 運行時_子錯誤_代碼</span> </td> 
   <td colname="5"> <p>低級AVE庫發出錯誤。 </p> <p>請參閱 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的詳細資訊</a> 的子菜單。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>實例化AVE低級庫時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>釋放AVE低級庫時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>釋放AVE庫使用的GPU資源時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>重置AVE庫時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>將視圖附加到AVE庫時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>備用音頻</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> 下載錯誤 </span> </td> 
   <td colname="4"><span class="codeph"> 音頻軌道名稱 </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> <p>發生與音頻軌道相關的錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>泛型</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999 </span> </td> 
   <td colname="2"><span class="codeph"> 泛型_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>標籤泛型錯誤事件。 不是TVSDK發的。 它只是TVSDK錯誤事件所對應的數字代碼範圍末尾的標籤。 </p> </td> 
  </tr> 
 </tbody> 
</table>
