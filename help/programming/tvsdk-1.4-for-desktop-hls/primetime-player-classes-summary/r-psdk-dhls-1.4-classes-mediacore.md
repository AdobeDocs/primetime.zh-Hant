---
description: 您可以使用Primetime Player API來自訂播放器的行為。 這些類別會描述您的媒體播放器及其資源。
title: Mediacore類別
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Mediacore類{#mediacore-classes}

您可以使用Primetime Player API來自訂播放器的行為。 這些類別會描述您的媒體播放器及其資源。

若要查看TVSDK的完整API檔案，請至[Adobe PrimetimeAPI參考](https://help.adobe.com/en_US/primetime/api/index.html)。

這些類別會說明您的媒體播放器及其資源。
套件：[com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/package-detail.html)

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
   <td colname="2"> 封裝所有自適應位速率控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a></span> </td> 
   <td colname="2"> 封裝所有緩衝區控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionStyles.html" format="html" scope="external"> ClosedCaptionsStyles</a></span> </td> 
   <td colname="2"> 定義隱藏字幕中文字所有樣式屬性的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionsVisibility.html" format="html" scope="external"> ClosedCaptionsVisibility</a></span> </td> 
   <td colname="2"> 控制隱藏字幕是否可見的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ContentFactory.html" format="html" scope="external"> ContentFactory</a> </span> </td> 
   <td colname="2"> 用於建立和管理廣告工作流中使用的各種元件的工廠基礎類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 廣告播放行為的預設實作。 允許應用程式自訂廣告行為的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultContentFactory.html" format="html" scope="external"> DefaultContentFactory</a></span> </td> 
   <td colname="2">預設實作<span class="codeph"> MediaPlayerClient</span>工廠，同時支援中繼資料和廣告解析程式。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2"><span class="codeph"> MediaPlayer</span>介面的預設類別實作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerConfig.html" format="html" scope="external"> DefaultMediaPlayerConfig</a> </span> </td> 
   <td colname="2"> 媒體播放器預設實作的設定類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 預設媒體播放器項目設定類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemLoader.html" format="html" scope="external"> DefaultMediaPlayerItemLoader</a></span> </td> 
   <td colname="2"> 預設媒體播放器項目載入器。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a></span> </td> 
   <td colname="2"><span class="codeph"> DefaultMediaPlayer</span>類別的公用介面。 包含事件、PlayerState和可見性的枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerConfig.html" format="html" scope="external"> MediaPlayerConfig</a> </span> </td> 
   <td colname="2"> 媒體播放器設定類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerContext.html" format="html" scope="external"> MediaPlayerContext</a></span> </td> 
   <td colname="2"> 提供媒體播放器其他內容的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a></span> </td> 
   <td colname="2"> 代表音訊——視訊媒體的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 預設媒體播放器項目設定類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a></span> </td> 
   <td colname="2">載入媒體播放器資源並建立對應<span class="codeph"> MediaPlayerItem</span>物件的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerStatus.html" format="html" scope="external"> MediaPlayerStatus</a></span> </td> 
   <td colname="2"> 包含媒體播放器支援狀態的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a></span> </td> 
   <td colname="2"><span class="codeph"> MediaPlayer</span>用於視訊演算的檢視類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a></span> </td> 
   <td colname="2"> 包含媒體資源所有資訊的類別。 包括媒體資源類型枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResourceType.html" format="html" scope="external"> MediaResourceType</a></span> </td> 
   <td colname="2"> 包含支援的介質資源類型的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a></span> </td> 
   <td colname="2"> 除了預設提示標籤外，封裝媒體播放器在執行廣告放置時所使用之自訂標籤的類別。 它也包含應用程式想要收到通知的標籤名稱。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> TextFormat</a></span> </td> 
   <td colname="2"> 封裝描述文字樣式的不同屬性（例如隱藏字幕樣式）的介面。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 版本</a></span> </td> 
   <td colname="2"> 提供TVSDK版本與說明的類別。 </td> 
  </tr> 
 </tbody> 
</table>

