---
description: 此表提供了有關ERROR類型通知的詳細資訊。
title: 錯誤通知代碼
exl-id: dc65670e-4764-4d68-aee1-87b2d27b09b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 5%

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
   <td colname="5"></td> 
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
   <td colname="3"></td> 
   <td colname="4"></td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101001 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_PLAYBACK_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> 內部錯誤 </span><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> 查找錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明</span> </td> 
   <td colname="5"> <p>執行查找操作時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> 暫停_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>執行暫停操作時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101101 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> 播放器未就緒 </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>  </p> <p>  </p>
    <!-- workaround for PDF having too much negative kerning in column 2 --> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>資源無效</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102000 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_MEDIA_PLAYER_ITEM </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告處理</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_無效 </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED</span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>由於無效的ad-metadata格式，廣告解析失敗。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> <span class="codeph"> AD_NOT_INSERTED </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
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
   <td colname="4"> <span class="codeph"> 內部錯誤 </span> </td> 
   <td colname="5"> <p>發生低級iOS錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>配置</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>嘗試更改抄送軌道的可見性時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_錯誤 </span> </td> 
   <td colname="3"> <span class="codeph"> 本機錯誤 </span> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>嘗試更改抄送軌道的樣式選項時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>iOS</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_HLS_VERSION_不相容 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>HLS版廣告比HLS版內容高。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170001 </span> </td> 
   <td colname="2"><span class="codeph"> 參數_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>參數錯誤 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170002 </span> </td> 
   <td colname="2"><span class="codeph"> M3U8_PARSER_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>無法分析m3u8。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170003 </span> </td> 
   <td colname="2"><span class="codeph"> WEBVTT_PARSER_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>無法分析Webvtt。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170004 </span> </td> 
   <td colname="2"><span class="codeph"> HLS_SEGMENT_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> URL </span><span class="codeph"> 內部錯誤 </span> </td> 
   <td colname="5"> <p>段超出了變數的指定頻寬。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170005 </span> </td> 
   <td colname="2"><span class="codeph"> MBR_MEDIASEQUENCE_OFFSYNC </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>此MBR的所有HLS流上的媒體序列號未同步。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170006 </span> </td> 
   <td colname="2"><span class="codeph"> MISSING_FILE_ERROR </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span><span class="codeph"> URL </span><span class="codeph"> 內部錯誤 </span> </td> 
   <td colname="5"> <p>缺少檔案或未響應。 </p> <p>HTTP 404:找不到檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170007 </span> </td> 
   <td colname="2"><span class="codeph"> AD_EMPTY_RESPONSE </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>無法檢索廣告。 空響應。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TIMEOUT </span> </td> 
   <td colname="3"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>無法檢索廣告。 超時錯誤。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170009 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> 播放器未就緒 </span> </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> <p>更改字幕通道時出錯。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170010 </span> </td> 
   <td colname="2"><span class="codeph"> SiteCatalyst_錯誤 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 說明 </span> </td> 
   <td colname="5"> <p>站點催化劑錯誤。 請參閱說明。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 170011 </span> </td> 
   <td colname="2"><span class="codeph"> AD_TARGET_DURATION_INCOMPLATIVE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> AD_ASSET</span> </td> 
   <td colname="5"> <p>廣告的TARGET DURATION高於內容的TARGET DURATION。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>可以通過 `PTAdAsset` 在通知元資料中 `AD_ASSET` 按鈕
