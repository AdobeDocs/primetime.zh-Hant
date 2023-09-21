---
description: 您可以設定播放器以追蹤和分析視訊使用情況。
title: 初始化和設定視訊分析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 初始化和設定視訊分析{#initialize-and-configure-video-analytics}

您可以設定播放器以追蹤和分析視訊使用情況。

在啟用視訊追蹤（視訊心率）之前，請確定您擁有下列專案：

* 適用於案頭HLS的TVSDK
* 設定/初始化資訊 — 請聯絡您的Adobe代表，取得您特定的視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> AppMeasurement追蹤伺服器端點 </td> 
   <td colname="col2"> Adobe Analytics (先前稱為SiteCatalyst)後端收集端點的URL。 </td> 
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
  <tr> 
   <td colname="col1"> 訪客追蹤伺服器端點 </td> 
   <td colname="col2"> 為目前視訊檢視器提供唯一識別碼的後端端點URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 發佈者 </td> 
   <td colname="col2"> 這是發佈者ID，由客戶的Adobe代表提供給客戶。 <p>提示：此ID不只具有品牌/電視名稱的字串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

若要在播放器中設定視訊追蹤：

1. 例項化及設定VisitorAPI程式庫。

       請牢記以下資訊：
   
   * 具現化需要由Adobe提供的Marketing Cloud組織ID輸入引數。

     這是字串值。
   * VisitorAPI程式庫的唯一設定選項是後端端點的URL，可提供目前使用者的唯一識別碼。
   * 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。

     如需實作訪客ID服務的相關資訊，請參閱訪客ID服務實作。

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. 例項化及設定AppMeasurement元件。

   AppMeasurement執行個體有許多設定選項。 如需詳細資訊，請參閱 [Adobe Analytics開發人員](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 檔案。 下列範常式式碼中的選項( `account`， `visitorNamespace`、和 `trackingServer`)為必填欄位，而值則由Adobe提供。

   >[!IMPORTANT]
   >
   >您必須確保相依性鏈結已正確設定。 AppMeasurement例項會彙總（取決於）訪客API元件。

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
   >在您的應用程式中，確認 `appMeasurementObject.visitor` 會在起始video analytics流程之前填入，否則您可能無法取得任何追蹤結果。 這些結果由記錄中的訊息指示。 您可以新增空白追蹤呼叫( `appMeasurementObject.track`)，輪詢 `visitor` 屬性，直到填入為止，並啟動視訊分析。

1. 初始化和設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組midstream，並視需要再次將其重新初始化。 在重新初始化模組之前，請確定視訊分析中繼資料也更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複子步驟1和2。

   1. 建立Video Analytics中繼資料的例項。

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

   1. 將Video Analytics中繼資料新增至全域中繼資料例項。

      準備就緒後，請在媒體資源或媒體播放器專案上設定全域中繼資料例項：

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. 初始化Video Analytics追蹤器

      建立媒體播放器例項後，您必須建立Video Analytics追蹤器例項，並提供媒體播放器例項的參考。

      >[!TIP]
      >
      >請一律為每個內容播放工作階段建立新的追蹤器例項，並在您分離媒體播放器例項後移除先前的參照。

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. 銷毀Video Analytics追蹤器。

      開始新的內容播放工作階段之前，請先摧毀視訊追蹤器的上一個例項。 收到內容完成事件（或通知）後，請稍候幾分鐘再摧毀視訊追蹤器例項。 立即摧毀執行個體可能會干擾Video Analytics追蹤器傳送視訊完成Ping的功能。

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. 手動將即時/線性資料流標示為完成。

      如果您在一個即時資料流上有各種集數，您可以使用完整的API手動將集數標示為完成。 這會結束目前影片的視訊追蹤工作階段，而且您可以為下一集開始新的追蹤工作階段。

      >[!TIP]
      >
      >此API為選用專案，VOD視訊追蹤不需要此API。
