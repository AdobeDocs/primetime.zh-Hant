---
description: 您可以配置播放器以跟蹤和分析視頻使用。
title: 初始化和配置視頻分析
exl-id: 82013882-e314-44fd-82f2-0640575d3c68
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 初始化和配置視頻分析{#initialize-and-configure-video-analytics}

您可以配置播放器以跟蹤和分析視頻使用。

在激活視頻跟蹤（視頻心跳）之前，請確保您有以下幾點：

* 用於Android的TVSDK
* 配置/初始化資訊 — 有關特定視頻跟蹤帳戶資訊，請與Adobe代表聯繫：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>重要提示：此JSON配置檔案名必須保留 <span class="codeph"> ADBMobileConfig.json </span>。 無法更改此配置檔案的名稱和路徑。 此檔案的路徑必須為 <span class="codeph"> &lt;source root=""&gt;/assets </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement跟蹤伺服器終結點 </td> 
   <td colname="col2"> Adobe Analytics(以前為SiteCatalyst)後端集合終結點的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 視頻分析跟蹤伺服器終結點 </td> 
   <td colname="col2"> 視頻分析後端集合終結點的URL。 這是發送所有視頻心跳跟蹤呼叫的地方。 <p>提示：訪問者跟蹤伺服器的URL與分析跟蹤伺服器的URL相同。 有關實施訪問者ID服務的資訊，請參見 <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> 實施ID服務 </a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帳戶名 </td> 
   <td colname="col2"> 也稱為報告套件ID(RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud組織ID </td> 
   <td colname="col2"> 實例化訪問者元件所需的字串值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 發佈者 </td> 
   <td colname="col2"> 這是發佈者ID，由客戶的Adobe代表提供給客戶。 <p>提示：此ID不僅是帶有品牌/電視名稱的字串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

要在播放器中配置視頻跟蹤，請執行以下操作：

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

   此JSON格式的配置檔案與TVSDK捆綁為資源。 播放器僅在載入時讀取這些值，並且這些值在應用程式運行時保持不變。

   要配置載入時間選項：

   1. 確認 `ADBMobileConfig.json` 檔案包含由Adobe提供的相應值。
   1. 確認此檔案位於 `assets` 的子菜單。

      此資料夾必須位於應用程式源樹的根中。
   1. 編譯並構建應用程式。
   1. 部署並運行捆綁的應用程式。

      有關這些AppMeasurement設定的詳細資訊，請參見 [Adobe Analytics視頻測量](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en)。
1. 初始化和配置視頻心跳跟蹤元資料。

   >[!IMPORTANT]
   >
   >您可以停止視頻分析模組中流，並根據需要重新初始化它。 在重新初始化模組之前，請確保視頻分析元資料也更新為正確的內容元資料。 要重新建立元資料，請重複子步驟1和2。

   1. 建立視頻分析元資料的實例。

      此實例包含啟用視頻心跳跟蹤所需的所有配置資訊。 例如：

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

   1. 將視頻分析元資料添加到全局元資料實例。

      準備好後，在媒體資源或媒體播放器項目上設定全局元資料實例：

      ```java
      ((MetadataNode)resourceMetadata).setNode( 
            DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY.getValue(), vaMetadata);
      ```

   1. 初始化視頻分析跟蹤器。

      建立媒體播放器實例後，必須建立視頻分析跟蹤器實例並提供對媒體播放器實例的引用。

      >[!TIP]
      >
      >始終為每個內容播放會話建立新的跟蹤器實例，並在分離媒體播放器實例後刪除以前的引用。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider =  
        new VideoAnalyticsProvider(appContext); 
      
      // Attach the TVSDK media player instance 
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 銷毀視頻分析跟蹤器。

      在開始新的內容播放會話之前，請銷毀視頻跟蹤器的先前實例。 收到內容完成事件（或通知）後，請等待幾分鐘，然後銷毀視頻跟蹤器實例。 立即銷毀實例可能會干擾視頻分析跟蹤程式發送視頻完成ping的能力。

      ```java
      if (_videoAnalyticsProvider) { 
          _videoAnalyticsProvider.detachMediaPlayer(); 
          _videoAnalyticsProvider = null; 
      }
      ```

   1. 手動將Live/Linear流標籤為完成。

      如果您在一個即時流上有各種集數，則可以使用完整的API手動將集數標籤為完整。 這將結束當前視頻集的視頻跟蹤會話，並且您可以為下一集啟動新的跟蹤會話。

      >[!TIP]
      >
      >此API是可選的，不需要用於VOD視頻跟蹤。

      ```java
      if (_videoAnalyticsProvider) { 
         _videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
