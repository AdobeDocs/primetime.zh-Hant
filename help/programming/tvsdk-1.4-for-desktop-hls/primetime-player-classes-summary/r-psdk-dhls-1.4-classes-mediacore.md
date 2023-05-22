---
description: 可以使用Mogfire Player API自定義播放器的行為。 這些類描述媒體播放器及其資源。
title: 媒體類
exl-id: 8948484d-a48d-49b4-ac11-b68f1abaf706
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# 媒體類{#mediacore-classes}

可以使用Mogfire Player API自定義播放器的行為。 這些類描述媒體播放器及其資源。

要查看TVSDK的完整API文檔，請轉至 [Adobe PrimetimeAPI參考](https://help.adobe.com/en_US/primetime/api/index.html)。

這些類描述媒體播放器及其資源。
包： [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>名稱 </p> </th> 
   <th colname="2" class="entry"> <p>說明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a> </span> </td> 
   <td colname="2"> 封裝所有自適應比特率控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a></span> </td> 
   <td colname="2"> 封裝所有緩衝區控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionStyles.html" format="html" scope="external"> 隱藏字幕樣式</a></span> </td> 
   <td colname="2"> 定義隱藏字幕中文本的所有樣式屬性的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionsVisibility.html" format="html" scope="external"> 隱藏字幕可見性</a></span> </td> 
   <td colname="2"> 控制隱藏字幕是否可見的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ContentFactory.html" format="html" scope="external"> 內容工廠</a> </span> </td> 
   <td colname="2"> 用於建立和管理廣告工作流中使用的各種元件的工廠基類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 廣告播放行為的預設實現。 允許應用程式自定義廣告行為的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultContentFactory.html" format="html" scope="external"> 預設內容工廠</a></span> </td> 
   <td colname="2">預設實現 <span class="codeph"> MediaPlayer客戶端</span> 工廠為元資料和解析過程提供支援。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> 預設媒體播放器</a></span> </td> 
   <td colname="2">預設類實現 <span class="codeph"> 媒體播放器</span> 。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerConfig.html" format="html" scope="external"> 預設媒體播放器配置</a> </span> </td> 
   <td colname="2"> 媒體播放器預設實現的配置類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 預設媒體播放器項配置類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemLoader.html" format="html" scope="external"> DefaultMediaPlayerItemLoader</a></span> </td> 
   <td colname="2"> 預設媒體播放器項載入器。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> 媒體播放器</a></span> </td> 
   <td colname="2">的公共介面 <span class="codeph"> 預設媒體播放器</span> 類。 包括Event、PlayerState和Visibility的枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerConfig.html" format="html" scope="external"> 媒體播放器配置</a> </span> </td> 
   <td colname="2"> 媒體播放器配置類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerContext.html" format="html" scope="external"> 媒體播放器上下文</a></span> </td> 
   <td colname="2"> 為媒體播放器提供附加上下文的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> 媒體播放器項</a></span> </td> 
   <td colname="2"> 表示音頻 — 視頻媒體的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 預設媒體播放器項配置類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a></span> </td> 
   <td colname="2">載入媒體播放器資源並建立相應的 <span class="codeph"> 媒體播放器項</span> 的雙曲餘切值。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerStatus.html" format="html" scope="external"> 媒體播放器狀態</a></span> </td> 
   <td colname="2"> 包含媒體播放器支援狀態的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> 媒體播放器視圖</a></span> </td> 
   <td colname="2">將由 <span class="codeph"> 媒體播放器</span> 顯示。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> 媒體資源</a></span> </td> 
   <td colname="2"> 包含有關媒體資源的所有資訊的類。 包括媒體資源類型的枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResourceType.html" format="html" scope="external"> 媒體資源類型</a></span> </td> 
   <td colname="2"> 包含支援的媒體資源類型的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKonfig</a></span> </td> 
   <td colname="2"> 除預設提示標籤外，還封裝媒體播放器在執行廣告放置時使用的自定義標籤的類。 它還包括應用程式要通知的標籤名稱。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> 文本格式</a></span> </td> 
   <td colname="2"> 封裝描述文本樣式的不同屬性（例如，隱藏字幕樣式）的介面。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 版本</a></span> </td> 
   <td colname="2"> 提供TVSDK版本和說明的類。 </td> 
  </tr> 
 </tbody> 
</table>
