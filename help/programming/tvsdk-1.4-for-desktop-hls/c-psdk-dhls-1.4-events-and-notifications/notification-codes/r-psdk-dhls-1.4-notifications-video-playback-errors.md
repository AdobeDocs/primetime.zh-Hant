---
description: AVE的Video Encoder介面在NATIVE_ERROR元資料對象中返回這些視頻回放通知。
title: NATIVE_ERROR視頻播放值
exl-id: 8e6ea6f8-bef2-4000-97a5-8d14c165079e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 6%

---

# 本機錯誤(_E):視頻播放值{#native-error-video-playback-values}

AVE的Video Encoder介面在NATIVE_ERROR元資料對象中返回這些視頻回放通知。

<table> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> RUNTIME_CODE元資料鍵的值 </th> 
   <th colname="col2" class="entry"> RUNTIME_CODE_MESSAGE元資料鍵的值 </th> 
   <th colname="col3" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> 期末</span> </td> 
   <td colname="col3"> 期末。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> 成功</span> </td> 
   <td colname="col3"> 操作成功。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> 非同步操作。 已發出操作請求。 以後將提供成功/失敗資訊。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> 由於檔案結束(EOF)條件，無法執行操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> 解碼器失敗</span> </td> 
   <td colname="col3"> 解碼器在運行時失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> 設備開啟錯誤</span> </td> 
   <td colname="col3"> 無法開啟硬體解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> 找不到檔案 </span> </td> 
   <td colname="col3"> 找不到資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> 泛型_錯誤 </span> </td> 
   <td colname="col3"> 一般錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> 不可恢復_錯誤 </span> </td> 
   <td colname="col3"> 視頻引擎無法從中恢復的錯誤條件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> 網路錯誤，正在嘗試恢復。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> 無固定大小 </span> </td> 
   <td colname="col3"> 無法確定資源的大小。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> 未實現(_I) </span> </td> 
   <td colname="col3"> 功能未實現。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> 記憶體不足 </span> </td> 
   <td colname="col3"> 記憶體不足。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> 分析錯誤 </span> </td> 
   <td colname="col3"> 分析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> 大小未知 </span> </td> 
   <td colname="col3"> 資源有大小，但未知。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> 下(_F) </span> </td> 
   <td colname="col3"> 下流情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_配置 </span> </td> 
   <td colname="col3"> 不支援配置。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> 不支援的_OPERATION </span> </td> 
   <td colname="col3"> 不支援操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> 等待初始化 </span> </td> 
   <td colname="col3"> 尚未初始化。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> 無效參數 </span> </td> 
   <td colname="col3"> 參數無效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> 不允許操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> 僅在暫停時允許該操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> 操作不能僅用於音頻檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> 上一尋道操作仍在進行中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> 未指定源 </span> </td> 
   <td colname="col3"> 未指定資源。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> 範圍_錯誤</span> </td> 
   <td colname="col3"> 指定的值超出範圍。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> 無效_SEEK_TIME</span> </td> 
   <td colname="col3"> 無效的查找時間。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> 指定的檔案不符合預期語法。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> 元件建立失敗</span> </td> 
   <td colname="col3"> 無法建立基本元件。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> 無法建立DRM上下文。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> 不支援容器類型。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> 查找失敗</span> </td> 
   <td colname="col3"> 查找失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的編解碼器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> 網路不可用</span> </td> 
   <td colname="col3"> 網路不可用。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> 網路錯誤</span> </td> 
   <td colname="col3"> 從網路獲取資料時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> 溢出</span> </td> 
   <td colname="col3"> 溢出。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> 支援VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> 不支援的視頻配置檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> 期間未載入</span> </td> 
   <td colname="col3"> 嘗試在HOLD期間或尚未載入的期間執行操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> 無效_REPLACE_DURATION</span> </td> 
   <td colname="col3"> 指定的替換持續時間無效或延伸到流的末尾。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> 調用的_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> 無法從錯誤的線程調用API。 大多數情況下，應僅從主線程調用的API元素。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> 片段讀取錯誤。 不存在故障轉移。 引擎將嘗試讀取下一個片段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> 中止</span> </td> 
   <td colname="col3"> 該操作被顯式中止或銷毀調用中止。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> 無法播放此版本的HLS媒體。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> 無法故障轉移。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP下載超時。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> 網路(_D) </span> </td> 
   <td colname="col3"> 用戶的網路連接已關閉。 播放可以隨時停止，並在連接可用時恢復。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> 在流中找不到可用比特率配置檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> 清單的簽名錯誤。 未通過清單簽名test。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> 無法載入播放清單。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> 替換失敗</span> </td> 
   <td colname="col3"> 在插入API中指定的替換無法成功。 這意味著插入成功，但替換未成功。 如果要替換的清單已從時間線中刪除，則替換可能失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM正在切換到非對稱配置檔案。 所有配置檔案預計在持續時間內對齊。 否則，將引發此警告，並且回放中可能出現跳轉。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> 「即時」窗口只能向前移動。 否則，將引發此警告，並且不會讀取窗口。 因此，回放中可能會出現跳轉（或停止/長暫停）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> 當前期間已到期</span> </td> 
   <td colname="col3"> 即時窗口已超出當前時段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> 內容長度不匹配</span> </td> 
   <td colname="col3"> HTTP伺服器報告的內容長度與實際媒體大小不匹配。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> 期間_保持</span> </td> 
   <td colname="col3"> 介質讀取器無法進一步讀取，因為它已達到由 <span class="codeph"> 設定保留位置</span> API。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> 即時保留(_H) </span> </td> 
   <td colname="col3"> 介質讀取器無法載入段，因為它已到達即時窗口的末尾。 當伺服器將新媒體廣告到即時窗口時，將恢復段載入。 通常在以下情況下達到此狀態： 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">的 <span class="codeph"> 緩衝區時間</span> 過高（等於或高於即時窗口持續時間）。 </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">一個或多個插入/擦除API的組合替換了比它添加的介質多的介質。 </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">下一個時段是等待介質更換的即時時段(由於 <span class="codeph"> 插入方式</span> API調用) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEARG </span> </td> 
   <td colname="col3"> 媒體中的音頻和視頻交織操作不正確。 這是打包錯誤。 當差值超過兩秒時，將發出警告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> 播放_未授權</span> </td> 
   <td colname="col3"> 未在Flash Player中啟用HLS回放。 請參閱 <span class="codeph"> AuthorizedFeatures.enableHLSPlayback</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> 解碼器接收了無法解碼的壞樣本。 這通常不是致命錯誤，但表示音頻/視頻中可能出現故障。 此錯誤的實例過多表示編碼錯誤或檔案錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> 播放開始後，「插入/替換」範圍不應包含讀取頭。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTURL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> 在即時媒體上不允許插入卷後。 但是，在伺服器將介質標籤為完整後，才允許使用這些介質。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> 內部錯誤</span> </td> 
   <td colname="col3"> 這是一個非常罕見的，不該發生的問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> 流不遵循始終將H264 SPS/PPS放入AVCC的打包建議。 可能發現查找/播放問題。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> 部分替換</span> </td> 
   <td colname="col3"> 在插入API中指定的替換操作僅部分完成。 當replaceDuration跨越時間軸持續時間時會發生這種情況。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> 載入格式副本播放清單時出錯。 這隻適用於AVE，而不適用於FlashPlayer。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> 操作不執行任何操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKPIPED_ON_FAILURE</span> </td> 
   <td colname="col3"> 無法播放段，失敗時會跳過段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> 不相容的RENDER_MODE</span> </td> 
   <td colname="col3"> 不相容的呈現模式。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> 不支援URL中使用的Web協定。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPLATIVE_VERSION</span> </td> 
   <td colname="col3"> 分析媒體檔案時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> 清單_檔案_意外_更改</span> </td> 
   <td colname="col3"> 清單檔案以意外方式更改。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間線執行拆分操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> 無法對時間線執行擦除操作。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_NEXT_FRAGMENTGET</span> </td> 
   <td colname="col3"> 沒有找到下一個碎片。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> 無時間軸</span> </td> 
   <td colname="col3"> 內部資料結構中不存在時間線。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> 未找到監聽器</span> </td> 
   <td colname="col3"> 在內部資料結構中找不到偵聽器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> 無法啟動音頻。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> 無音頻接收器</span> </td> 
   <td colname="col3"> 內部資料結構中不存在音頻接收器。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> 檔案_開啟_錯誤</span> </td> 
   <td colname="col3"> 無法開啟檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> 檔案寫入錯誤</span> </td> 
   <td colname="col3"> 無法寫入檔案。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> 檔案讀取錯誤</span> </td> 
   <td colname="col3"> 無法從檔案讀取。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> 分析ID3資料時出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> 安全性_錯誤 </span> </td> 
   <td colname="col3"> 由於安全限制，載入內容失敗。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> 時間軸太短</span> </td> 
   <td colname="col3"> 時間線持續時間太短。 如果這是即時流，則可能會發生頻繁的緩衝。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> 該流已切換為僅音頻流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> 該流已從僅音頻切換到帶視頻的流。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> 未找到鍵 </span> </td> 
   <td colname="col3"> 找不到密鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> 無效鍵</span> </td> 
   <td colname="col3"> 密鑰無效。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> 密鑰伺服器不返回密鑰。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> 無法處理主清單更新。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> URCERTED_TIME_DISCUNTIATION_FOUND</span> </td> 
   <td colname="col3"> 發現未報告的時間中斷。 </td> 
  </tr> 
 </tbody> 
</table>
