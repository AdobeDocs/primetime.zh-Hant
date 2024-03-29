---
title: PSDK錯誤碼
description: 有關各種錯誤碼、警告和原生錯誤碼的資訊。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 6%

---

# PSDK錯誤碼 {#psdk-error-codes}

請閱讀下文，瞭解PSDK錯誤代碼、警告及原生錯誤代碼。

## 錯誤

下表提供有關ERROR型別通知的詳細資訊。 大多數錯誤包含相關的中繼資料，例如無法下載的資源的URL。 有些通知包含中繼資料，用於指定問題發生在主要視訊內容、替代音訊內容還是廣告中。

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>PSDK錯誤名稱</b></th>
   <th><b>PSDK錯誤碼</b></th>
   <th><b>說明</b></th>
  </tr>
  <tr>
    <td>成功</td>
    <td>0</td>
    <td>由基礎API執行的操作成功。</td>
  </tr>
  <tr>
    <td>INVALID_ARGUMENT</td>
    <td>1</td>
    <td>提供給基礎API的資料或引數格式無效。</td>
  </tr>
  <tr>
    <td>NULL_POINTER</td>
    <td>2</td>
    <td>其中一個傳入的引數為NULL，或者其中一個內部成員未初始化。</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>目前的播放器狀態不支援此操作。</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>當要求的介面不是由此實作/繼承時，interfaceCast方法會擲回此錯誤。</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>建立其中一個內部資源失敗。</td>
  </tr>
  <tr>
    <td>不支援的操作</td>
    <td>6</td>
    <td>目前不支援要求的操作。</td>
  </tr>
  <tr>
    <td>DATA_NOT_AVAILABLE</td>
    <td>7</td>
    <td>要求的資料目前無法使用。</td>
  </tr>
  <tr>
    <td>SEEK_ERROR</td>
    <td>8</td>
    <td>執行搜尋作業時發生錯誤。</td>
  </tr>
  <tr>
    <td>不支援的功能</td>
    <td>9</td>
    <td>不支援此功能。</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>10</td>
    <td>指定的值超出範圍。</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORT</td>
    <td>11</td>
    <td>TVSDK或基礎裝置不支援指定資料流的音訊/視訊轉碼器。</td>
  </tr>
  <tr>
    <td>MEDIA_ERROR</td>
    <td>12</td>
    <td>找不到指定的媒體。</td>
  </tr>
  <tr>
    <td>NETWORK_ERROR</td>
    <td>13</td>
    <td>下載片段或區段（視訊和音訊）時發生錯誤。</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>14</td>
    <td>一般錯誤事件。 並非由TVSDK實際發行。 這僅是與TVSDK錯誤事件相對應的數值代碼範圍結尾的標籤。</td>
  </tr>
  <tr>
    <td>無效的SEEK_TIME</td>
    <td>15</td>
    <td>提供的搜尋時間無效。</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>發生與音訊曲目相關的錯誤（替代音訊）</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>PSDK API是從不同執行緒呼叫，而不是從初始化PSDK的執行緒呼叫。</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>找不到元素。</td>
  </tr>
  <tr>
    <td>未實作</td>
    <td>19</td>
    <td>功能未實作。</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>已透過AdvertisingMetadata停用preroll。</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>Flash Player中尚未啟用HLS播放。 請參閱AuthorizedFeatures.enableMediaPlayerHLSPlayback()。</td>
  </tr>
  <tr>
    <td>NETWORK_TIMEOUT</td>
    <td>58</td>
    <td>擷取資源/連線伺服器時，網路逾時。</td>
  </tr>
</table>

## 警告

下表提供有關WARN型別通知的詳細資訊。
大多數警告包含相關的中繼資料，例如無法下載的資源的URL。 有些通知包含中繼資料，用於指定問題發生在主要視訊內容、替代音訊內容還是廣告中。

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>錯誤名稱</b></th>
    <th><b>程式碼</b></th>
    <th><b>說明</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>播放作業期間發生錯誤。 與播放相關的作業失敗</td>
  </tr>
  <tr>  
    <td>NATIVE_WARNING</td>
    <td>201</td>
    <td>低階AVE程式庫發生錯誤。</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>廣告外掛程式無法解析廣告。</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>無法載入廣告資訊清單。</td>
  </tr>
  <tr>
    <td>AD_RESOLUTION_IN_PROGRESS</td>
    <td>204</td>
    <td>解析廣告的作業正在進行中。</td>
  </tr>
  </table>

## 資訊

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>錯誤名稱</b></th>
    <th><b>程式碼</b></th>
    <th><b>說明</b></th>
  </tr>
  <tr>
    <td>REVENUE_OPTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>TVSDK詳細通知，以供進一步報告和分析。</td>
  </tr>
 </table>

## 原生錯誤代碼

AVE的視訊編碼器介面會在NATIVE_ERROR中繼資料物件中傳回這些視訊播放通知。

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>錯誤名稱</b></th>
    <th><b>程式碼</b></th>
    <th><b>說明</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>期間結束。</td>
  </tr>
  <tr>
    <td>成功</td>
    <td>0</td>
    <td>作業成功。</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>非同步操作。 已提出作業要求。 成功/失敗資訊將於稍後提供。</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>因為檔案結束(EOF)狀況而無法執行作業。</td>
  </tr>
  <tr>
    <td>解碼器失敗</td>
    <td>3</td>
    <td>解碼器在執行階段失敗。</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>無法開啟硬體解碼器。</td>
  </tr>
  <tr>
    <td>FILE_NOT_FOUND</td>
    <td>5</td>
    <td>找不到資源。</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>6</td>
    <td>一般錯誤。</td>
  </tr>
  <tr>
    <td>IRRECOVERABLE_ERROR</td>
    <td>7</td>
    <td>視訊引擎無法復原的錯誤狀況。</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERABLE</td>
    <td>8</td>
    <td>網路錯誤，正在嘗試復原。</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>無法判斷資源的大小。</td>
  </tr>
  <tr>
    <td>未實作</td>
    <td>10</td>
    <td>功能未實作。</td>
  </tr>
  <tr>
    <td>記憶體不足</td>
    <td>11</td>
    <td>記憶體不足。</td>
  </tr>
  <tr>
    <td>PARSE_ERROR</td>
    <td>12</td>
    <td>剖析媒體檔案時發生錯誤。</td>
  </tr>
  <tr>  
    <td>SIZE_UNKNOWN</td>
    <td>13</td>
    <td>資源有大小，但未知。</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>底流條件。</td>
  </tr>
  <tr> 
    <td>不支援的_CONFIG</td>
    <td>15</td>
    <td>不支援設定。</td>
  </tr>
  <tr>  
    <td>不支援的操作</td>
    <td>16</td>
    <td>不支援此操作。</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>尚未初始化。</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>無效的引數。</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>不允許作業。</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>只有在暫停時才允許此操作。</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>無法在僅限音訊的檔案上使用作業。</td>
  </tr>
  <tr>
    <td>上一步_步驟_搜尋_進行中</td>
    <td>22</td>
    <td>上一個搜尋作業仍在進行中。</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>未指定資源。</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>24</td>
    <td>指定的值超出範圍。</td>
  </tr>
  <tr>
    <td>無效的SEEK_TIME</td>
    <td>25</td>
    <td>無效的搜尋時間。</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>指定的檔案不符合預期的語法。</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILED</td>
    <td>27</td>
    <td>無法建立必要元件。</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>無法建立DRM內容。</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORT</td>
    <td>29</td>
    <td>不支援容器型別。</td>
  </tr>
  <tr>
    <td>搜尋失敗</td>
    <td>30</td>
    <td>搜尋失敗。</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORT</td>
    <td>31</td>
    <td>不支援的轉碼器。</td>
  </tr>
  <tr>
    <td>網路無法使用</td>
    <td>32</td>
    <td>網路無法使用。</td>
  </tr>
  <tr>  
    <td>NETWORK_ERROR</td>
    <td>33</td>
    <td>從網路取得資料時發生錯誤。</td>
  </tr>
  <tr>
    <td>溢位</td>
    <td>34</td>
    <td>溢位。</td>
  </tr>
  <tr>  
    <td>視訊設定檔不支援</td>
    <td>35</td>
    <td>不支援的視訊設定檔。</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>嘗試在HOLD期間或尚未載入的期間執行作業。</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>指定的取代持續時間無效或延伸超過資料流結尾。</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>無法從錯誤的執行緒呼叫API。 通常，只適用於應從主執行緒呼叫的API元素。</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_ERROR</td>
    <td>39</td>
    <td>片段讀取錯誤。 不存在容錯移轉。 引擎將嘗試讀取下一個片段。</td>
  </tr>
  <tr>
    <td>已中止</td>
    <td>40</td>
    <td>作業被明確的Abort或Destroy呼叫中止。</td>
  </tr>
  <tr>
    <td>不支援的_HLS_VERSION</td>
    <td>41</td>
    <td>無法播放此版本的HLS媒體。</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>無法容錯移轉。</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>HTTP下載已逾時。</td>
  </tr>
  <tr>
    <td>網路關閉</td>
    <td>44</td>
    <td>使用者的網路連線已中斷。 播放可能會隨時停止，並在連線可用時繼續。</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>在資料流中找不到可用的位元速率設定檔。</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>資訊清單的簽章錯誤。 資訊清單簽署測試失敗。</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>無法載入播放清單。</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>插入API中指定的取代無法成功。 這表示插入成功但取代失敗。 如果要取代的資訊清單已從時間軸移除，取代可能會失敗。</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMETRIC_PROFILE</td>
    <td>49</td>
    <td>DRM正在切換至非對稱輪廓。 所有設定檔預計都會在期間內對齊。 如果沒有，系統會擲回此警告，而且播放時可能會有跳躍。</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>即時視窗預期只會向前移動。 如果不會，系統會擲回此警告，且不會讀取視窗。 因此，播放中可能會出現跳躍（或停止/長時間暫停）。</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>即時視窗已移至目前期間以外。</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>HTTP伺服器報告的內容長度與實際媒體大小不符。</td>
  </tr>
  <tr>
    <td>PERIOD_HOLD</td>
    <td>53</td>
    <td>媒體讀取器無法進一步讀取，因為它已經達到setHoldAt API設定的時間。</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>媒體讀取器無法載入區段，因為它已經到達即時視窗的結尾。 伺服器向即時視窗新增媒體時，將會繼續載入區段。 達到此狀態通常發生於：<ul><li>bufferTime太高（等於或高於即時視窗持續時間）。</li><li>一或多個插入/清除API的組合取代的媒體多於新增的媒體。</li><li>下一個期間是有待處理媒體取代的即時期間（由於InsertBy API呼叫）</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>媒體中的音訊和視訊交錯處理不正確。 這是封裝錯誤。 當差異超過兩秒時會傳送警告。</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHORIZED</td>
    <td>57</td>
    <td>Flash Player中尚未啟用HLS播放。 請參閱AuthorizedFeatures.enableHLSPlayback。</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>解碼器收到無法解碼的錯誤樣本。 這通常不是嚴重錯誤，但表示音訊/視訊可能有問題。 此錯誤的例項太多，表示編碼錯誤或檔案錯誤。</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>開始播放後，插入/取代範圍不應包含讀取標頭。</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>即時媒體上不允許後置滾動插入。 但是，在伺服器將媒體標示為完成之後，就允許這些動作。</td>
  </tr>
  <tr>
    <td>INTERNAL_ERROR</td>
    <td>61</td>
    <td>這是一個絕不應該發生的問題。</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>資料流未遵循總是將H264 SPS/PPS放入AVCC的封裝建議。 可能會出現搜尋/播放問題。</td>
  </tr>
  <tr>  
    <td>PARTIAL_REPLACEMENT</td>
    <td>63</td>
    <td>插入API中指定的取代僅部分完成。 當replaceDuration跨越時間線持續時間時會發生這種情況。</td>
  </tr>
  <tr>
    <td>RENDITION_M3U8_ERROR</td>
    <td>64</td>
    <td>載入轉譯播放清單時發生錯誤。 這僅適用於AVE，不適用於FlashPlayer。</td>
  </tr>
  <tr>
    <td>NULL_OPERATION</td>
    <td>65</td>
    <td>操作沒有執行任何動作。</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>區段無法播放，因失敗已略過。</td>
  </tr>
  <tr>
    <td>不相容的_RENDER_MODE</td>
    <td>67</td>
    <td>不相容的轉譯模式。</td>
  </tr>
  <tr>
    <td>PROTOCOL_NOT_SUPPORT</td>
    <td>68</td>
    <td>不支援URL中使用的Web通訊協定。</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>剖析媒體檔案時發生錯誤。</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTLY_CHANGED</td>
    <td>70</td>
    <td>資訊清單檔案以非預期的方式變更。</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>無法在時間表上執行分割作業。</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>無法在時間表上執行清除操作。</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>未取得下一個片段。</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>內部資料結構中不存在時間軸。</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>在內部資料結構中找不到接聽程式。</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>無法啟動音訊。</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>內部資料結構中不存在音訊接收器。</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>無法開啟檔案。</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>無法寫入檔案。</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>無法從檔案讀取。</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>剖析ID3資料時發生錯誤。</td>
  </tr>
  <tr>
    <td>安全性_錯誤</td>
    <td>82</td>
    <td>由於安全性限制，載入內容失敗。</td>
  </tr>
  <tr>
    <td>時間軸_TOO_SHORT</td>
    <td>83</td>
    <td>時間表持續時間太短。 如果這是即時資料流，可能會發生頻繁的緩衝。</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>串流已切換為僅限音訊的串流。</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>串流已從純音訊切換為含有視訊的串流。</td>
  </tr>
  <tr>
    <td>KEY_NOT_FOUND</td>
    <td>87</td>
    <td>找不到金鑰。</td>
  </tr>
  <tr>
    <td>INVALID_KEY</td>
    <td>88</td>
    <td>金鑰無效。</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>金鑰伺服器未傳回金鑰。</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>無法處理主要資訊清單更新。</td>
  </tr>
  <tr>
    <td>未報告_時間_中斷_已找到</td>
    <td>91</td>
    <td>發現未回報的時間(PTS)中斷。</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>找到不相符的音訊和視訊中斷情形。</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>在特技播放模式中播放媒體時發生錯誤。 特技播放模式結束，資料流暫停。 呼叫Play()以正常模式播放媒體。</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>播放器已離開即時視窗，必須往前搜尋才能趕上進度。</td>
  </tr>
</table>
