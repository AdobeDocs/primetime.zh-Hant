---
description: 您可以使用Primetime Player API來自訂播放器的行為。
title: Mediacore類別
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Mediacore類{#mediacore-classes}

您可以使用Primetime Player API來自訂播放器的行為。

若要查看TVSDK的完整API檔案，請至[Adobe PrimetimeAPI參考](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)。

這些類別會說明您的媒體播放器及其資源。
套件：[com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>名稱 </p> </th> 
   <th colname="2" class="entry"> <p>說明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParametersABRControlParameters</a>  </span> </td> 
   <td colname="2"> 封裝所有自適應位速率控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdClientFactory.html" format="html" scope="external"> AdClientFactory</a> </span> </td> 
   <td colname="2"> 用於建立機會檢測器的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/AdvertisingFactory.html" format="html" scope="external"> AdvertisingFactory</a> </span> </td> 
   <td colname="2"> 允許自訂廣告決策程式的工廠類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a> </span> </td> 
   <td colname="2"> 封裝所有緩衝區控制參數的類。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 廣告播放行為的預設實作。 允許應用程式自訂廣告行為的介面。</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2"><span class="codeph"> MediaPlayer</span>介面的預設類別實作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a> </span> </td> 
   <td colname="2"><span class="codeph"> DefaultMediaPlayer</span>類別的公用介面。 包含事件、PlayerState和可見性的枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html" format="html" scope="external"> MediaPlayer.AdPlaybackEventListener</a></span> </td> 
   <td colname="2"> 廣告播放期間要呼叫的回呼集的介面定義。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html" format="html" scope="external"> MediaPlayer.DRMEventListener</a></span> </td> 
   <td colname="2"> 受保護中繼資料可用時要呼叫之回呼的介面定義。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.EventListener.html" format="html" scope="external"> MediaPlayer.EventListener</a> </span> </td> 
   <td colname="2"> 用於統一事件偵聽器註冊的標籤介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html" format="html" scope="external"> MediaPlayer.PlaybackEventListener</a> </span> </td>
   <td colname="2"> 播放期間要調用的一組回調的介面定義。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html" format="html" scope="external"> MediaPlayer.QOSEventListener</a> </span> </td> 
   <td colname="2"> QoS期間要調用的一組回調的介面定義。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a> </span> </td> 
   <td colname="2"> 代表音訊——視訊媒體的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a> </span> </td> 
   <td colname="2"> 載入媒體播放器資源並建立對應MediaPlayerItem物件的類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html" format="html" scope="external"> MediaPlayerItemLoader.LoaderListener</a> </span> </td> 
   <td colname="2"> 定義與MediaPlayerItemLoader物件關聯之監聽器方法的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a> </span> </td> 
   <td colname="2"> MediaPlayer用於視訊演算的檢視類別。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> MediaResource</a> </span> </td> 
   <td colname="2"> 包含媒體資源所有資訊的類別。 包括媒體資源類型枚舉。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PlacementOpportunityDetector.html" format="html" scope="external"> PlacementOpportunityDetector</a> </span> </td> 
   <td colname="2"> 用於處理資訊清單內提示的介面，此介面將用作廣告決策程式的位置。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a> </span> </td> 
   <td colname="2"> 除了預設提示標籤外，封裝媒體播放器在執行廣告放置時所使用之自訂標籤的類別。 它也包含應用程式想要收到通知的標籤名稱。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> TextFormat</a> </span> </td> 
   <td colname="2"> 封裝描述文字樣式的不同屬性（例如隱藏字幕樣式）的介面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/TextFormatBuilder.html" format="html" scope="external"> TextFormatBuilder</a></span> </td> 
   <td colname="2"> 設定文本格式的類方法。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 版本</a></span> </td> 
   <td colname="2"> 提供TVSDK版本與說明的類別。 </td> 
  </tr> 
 </tbody> 
</table>
