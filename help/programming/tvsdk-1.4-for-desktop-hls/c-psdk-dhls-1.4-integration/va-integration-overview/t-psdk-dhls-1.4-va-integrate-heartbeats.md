---
description: 您可以設定您的播放器來追蹤和分析視訊使用。
title: 初始化和設定視訊分析
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# 初始化並設定視訊分析{#initialize-and-configure-video-analytics}

您可以設定您的播放器來追蹤和分析視訊使用。

在啟動視訊追蹤（視訊心率）之前，請確定您有下列項目：

* Desktop HLS的TVSDK
* 設定／初始化資訊——請洽詢您的Adobe代表，以取得您的特定視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> AppMeasurement追蹤伺服器端點 </td> 
   <td colname="col2"> Adobe Analytics(之前稱為SiteCatalyst)後端收集端點的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 視訊分析追蹤伺服器端點 </td> 
   <td colname="col2"> 視訊分析後端收集端點的URL。 這是傳送所有視訊心率追蹤呼叫的地方。 <p>提示： 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。 如需實作訪客ID服務的詳細資訊，請參閱<a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external">實作ID服務</a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帳戶名稱 </td> 
   <td colname="col2"> 也稱為報表套裝ID(RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud組織ID </td> 
   <td colname="col2"> 執行個體化訪客元件所需的字串值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 訪客追蹤伺服器端點 </td> 
   <td colname="col2"> 提供目前視訊檢視器唯一識別碼的後端端點URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 發行者 </td> 
   <td colname="col2"> 這是發行者ID，由客戶的Adobe代表提供。 <p>提示： 此ID不僅是具有品牌／電視名稱的字串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

若要在您的播放器中設定視訊追蹤：

1. 執行個體化及設定VisitorAPI程式庫。

       請記住下列資訊：
   
   * 實例化需要Marketing Cloud組織ID輸入參數，該參數由Adobe提供。

      這是字串值。
   * VisitorAPI程式庫的唯一設定選項是後端端點的URL，可為目前使用者提供唯一識別碼。
   * 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。

      如需實作訪客ID服務的詳細資訊，請參閱訪客ID服務實作。

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. 執行個體化及設定AppMeasurement元件。

   AppMeasurement例項有許多設定選項。 如需詳細資訊，請參閱[Adobe Analytics開發人員](https://microsite.omniture.com/t2/help/en_US/reference/#Developer)檔案。 下列范常式式碼（`account`、`visitorNamespace`和`trackingServer`）中的選項為必要項，而值則由Adobe提供。

   >[!IMPORTANT]
   >
   >必須確保已正確設定從屬關係鏈。 AppMeasurement例項會匯總（視訪客API元件而定）。

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >在您的應用程式中，請確定在開始視訊分析流程之前已填入`appMeasurementObject.visitor`，否則可能無法取得任何追蹤結果。 這些結果由日誌中的消息指示。 您可以新增空的追蹤呼叫(`appMeasurementObject.track`)、輪詢`visitor`屬性，直到填入為止，並啟動視訊分析。

1. 初始化並設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組中間串流，並視需要重新初始化它。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複子步驟1和2。

   1. 建立視訊分析中繼資料的例項。

      此例項包含啟用視訊心率追蹤所需的所有設定資訊。 例如：

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. 將視訊分析中繼資料新增至全域中繼資料例項。

      當您準備好時，在媒體資源或媒體播放器項目上設定全域中繼資料例項：

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. 初始化視訊分析追蹤器。

      建立媒體播放器例項後，您必須建立視訊分析追蹤器例項並提供媒體播放器例項的參考。

      >[!TIP]
      >
      >請務必為每個內容播放作業建立新的追蹤器例項，並在您分離媒體播放器例項後移除先前的參考。

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. 銷毀視訊分析追蹤器。

      開始新的內容播放作業前，請先銷毀視訊追蹤器的先前例項。 收到內容完成事件（或通知）後，請等候幾分鐘，再銷毀視訊追蹤器例項。 立即銷毀執行個體可能會干擾視訊分析追蹤器傳送視訊完成ping的功能。

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. 手動將即時／線性串流標示為完成。

      如果您在一個即時串流上有不同的集數，您可以使用完整的API手動將集數標示為完整。 這會結束目前視訊集的視訊追蹤工作階段，而您可以開始下一集的新追蹤工作階段。

      >[!TIP]
      >
      >此API為選用API，不需要用於VOD視訊追蹤。

