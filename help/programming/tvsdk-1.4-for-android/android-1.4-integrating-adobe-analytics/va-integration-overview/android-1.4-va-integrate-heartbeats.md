---
description: 您可以設定您的播放器來追蹤和分析視訊的使用情形。
title: 初始化和設定視訊分析
exl-id: 82013882-e314-44fd-82f2-0640575d3c68
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 初始化和設定視訊分析{#initialize-and-configure-video-analytics}

您可以設定您的播放器來追蹤和分析視訊的使用情形。

在啟用視訊追蹤（視訊心率）之前，請確定您有下列項目：

* Android適用的TVSDK
* 設定/初始化資訊 — 請聯絡您的Adobe代表，取得您特定的視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>重要： 此JSON設定檔案名稱必須保留<span class="codeph"> ADBMobileConfig.json </span>。 無法更改此配置檔案的名稱和路徑。 此檔案的路徑必須是<span class="codeph"> &lt;source root&gt;/assets </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement追蹤伺服器端點 </td> 
   <td colname="col2"> Adobe Analytics(前身為SiteCatalyst)後端收集端點的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video Analytics追蹤伺服器端點 </td> 
   <td colname="col2"> video analytics後端收集端點的URL。 這是所有視訊心率追蹤呼叫的傳送位置。 <p>提示： 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。 如需實作訪客ID服務的相關資訊，請參閱<a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external">實作ID服務</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帳戶名稱 </td> 
   <td colname="col2"> 也稱為報表套裝ID(RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud組織ID </td> 
   <td colname="col2"> 具現化Visitor元件所需的字串值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 發佈者 </td> 
   <td colname="col2"> 這是發佈者ID，由客戶代表提供給Adobe。 <p>提示： 此ID不只是具有品牌/電視名稱的字串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

若要在播放器中設定視訊追蹤：

1. 確認`ADBMobileConfig.json`資源檔案中的載入時間選項正確。

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

   此JSON格式的設定檔案是與TVSDK搭配為資源。 您的播放器只會在載入時讀取這些值，而且當您的應用程式執行時，這些值會維持不變。

   要配置載入時間選項：

   1. 確認`ADBMobileConfig.json`檔案包含Adobe提供的適當值。
   1. 確認此檔案位於`assets`資料夾中。

      此資料夾必須位於應用程式源樹的根目錄中。
   1. 編譯並構建您的應用程式。
   1. 部署並運行捆綁的應用程式。

      如需這些AppMeasurement設定的詳細資訊，請參閱在Adobe Analytics中測量視訊[。](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en)
1. 初始化並設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組中繼，並視需要重新初始化。 重新初始化模組之前，請確定視訊分析中繼資料也更新為正確的內容中繼資料。 要重新建立元資料，請重複子步驟1和2。

   1. 建立Video Analytics中繼資料的例項。

      此例項包含啟用視訊心率追蹤所需的所有設定資訊。 例如：

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setPublisher("sample-publisher"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.quietMode = false; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. 將Video Analytics中繼資料新增至全域中繼資料例項。

      準備好後，請在媒體資源或媒體播放器項目上設定全域中繼資料例項：

      ```java
      ((MetadataNode)resourceMetadata).setNode( 
            DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY.getValue(), vaMetadata);
      ```

   1. 初始化Video Analytics追蹤器。

      建立媒體播放器例項後，您必須建立Video Analytics追蹤器例項，並提供媒體播放器例項的參考。

      >[!TIP]
      >
      >請務必為每個內容播放工作階段建立新的追蹤器例項，並在您分離媒體播放器例項後移除先前的參考。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider =  
        new VideoAnalyticsProvider(appContext); 
      
      // Attach the TVSDK media player instance 
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 銷毀Video Analytics追蹤器。

      開始新內容播放工作階段之前，請銷毀視訊追蹤器的先前例項。 收到內容完成事件（或通知）後，請等待幾分鐘再銷毀視訊追蹤器例項。 若立即銷毀例項，可能會干擾Video Analytics追蹤器傳送視訊完成Ping的功能。

      ```java
      if (_videoAnalyticsProvider) { 
          _videoAnalyticsProvider.detachMediaPlayer(); 
          _videoAnalyticsProvider = null; 
      }
      ```

   1. 手動將即時/線性資料流標示為完成。

      如果您的一個即時資料流上有各種集數，可以使用complete API手動將集數標示為已完成。 這會結束目前視訊集數的視訊追蹤工作階段，而您可以開始下一集的新追蹤工作階段。

      >[!TIP]
      >
      >此API為選用API，不是VOD視訊追蹤所需的API。

      ```java
      if (_videoAnalyticsProvider) { 
         _videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
