---
title: 初始化和設定視訊分析
description: 初始化和設定視訊分析
copied-description: true
exl-id: 26bdc11e-b8f6-414f-a3e9-53bc895d25ce
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 初始化和設定視訊分析 {#initialize-and-configure-video-analytics}

您可以設定播放器以追蹤和分析視訊使用情況。
在啟用視訊追蹤（視訊心率）之前，請確定您具備下列條件：

* 適用於Android的TVSDK 3.0。
* 設定/初始化資訊

   請聯絡您的Adobe代表，取得您的特定視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>重要：此JSON設定檔案名稱必須保留 <span class="filepath"> ADBMobileConfig.json </span>. 無法變更此設定檔的名稱和路徑。 此檔案的路徑必須是 <span class="filepath"> &lt;source root=""&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement追蹤伺服器端點 </td> 
   <td colname="col2"> Adobe Analytics (前身為SiteCatalyst)後端集合端點的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video Analytics追蹤伺服器端點 </td> 
   <td colname="col2"> 視訊分析後端集合端點的URL。 這是傳送所有視訊心率追蹤呼叫的位置。 <p>提示：訪客追蹤伺服器的URL與Analytics追蹤伺服器的URL相同。 如需實作訪客ID服務的相關資訊，請參閱 <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> 實作ID服務 </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帳戶名稱 </td> 
   <td colname="col2"> 也稱為報表套裝ID (RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud組織ID </td> 
   <td colname="col2"> 具現化訪客元件所需的字串值。 </td> 
  </tr> 
 </tbody> 
</table>

若要在播放器中設定視訊追蹤：

1. 確認中的載入時間選項 `ADBMobileConfig.json` 資源檔案正確。

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   此JSON格式設定檔案是隨TVSDK提供的資源。 您的播放器僅在載入時讀取這些值，而值在應用程式執行時保持不變。

   若要設定載入時間選項：


   1. 確認 `ADBMobileConfig.json` 檔案包含適當的值(由Adobe提供)。
   1. 確認此檔案位於 `assets/` 資料夾。

      此資料夾必須位於應用程式來源樹狀結構的根目錄中。

   1. 編譯及建置您的應用程式。
   1. 部署並執行隨附的應用程式。

      如需這些AppMeasurement設定的詳細資訊，請參閱 [在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. 初始化和設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止Video Analytics模組的Midstream，並視需要再次重新初始化。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複下列前兩個步驟（子步驟） **a** 和 **b**)。

   1. 建立Video Analytics中繼資料的例項。

      此例項包含啟用視訊心率追蹤所需的所有設定資訊。 例如：

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. 初始化Video Analytics提供者。

      建立媒體播放器例項後，您必須建立Video Analytics提供者例項，並提供其應用程式內容。

      >[!TIP]
      >
      >請一律為每個內容播放工作階段建立新的提供者例項，並在您分離媒體播放器例項後移除先前的參照。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. 在上設定視訊分析中繼資料 `videoAnalyticsProvider` 執行個體。

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. 將媒體播放器例項附加至 `videoAnalyticsProvider` 例項：

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 銷毀Video Analytics提供者。

      開始新的內容播放工作階段之前，請先銷毀視訊提供者的上一個例項。 收到內容完成事件（或通知）後，請稍候幾分鐘再銷毀視訊分析提供者執行個體。 立即摧毀執行個體可能會干擾Video Analytics提供者傳送「視訊完成」Ping的能力。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. 手動將即時/線性資料流標示為完成。

      如果您有一個即時資料流上有各種劇集，可以使用完整的API手動將劇集標示為完成。 如此將結束目前視訊集的視訊追蹤工作階段，而您可以為下一集開始新的追蹤工作階段。

      >[!TIP]
      >
      >此API為選用，不適用於VOD視訊追蹤。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
