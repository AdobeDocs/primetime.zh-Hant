---
description: 您可以設定您的播放器來追蹤和分析視訊的使用情形。
title: 初始化和設定視訊分析
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 初始化和設定視訊分析 {#initialize-and-configure-video-analytics}

您可以設定您的播放器來追蹤和分析視訊的使用情形。

在啟用視訊追蹤（視訊心率）之前，請確定您有下列項目：

* 設定/瀏覽器TVSDK初始化資訊 — 如需特定視訊追蹤帳戶資訊，請連絡您的Adobe代表：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
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
   <td colname="col1"> 訪客追蹤伺服器端點 </td>
   <td colname="col2"> 後端端點的URL，可提供目前視訊檢視器的唯一識別碼。 </td>
  </tr>
  <tr>
   <td colname="col1"> 發佈者 </td>
   <td colname="col2"> 這是發佈者ID，由客戶代表提供給Adobe。 <p>提示： 此ID不只是具有品牌/電視名稱的字串。 </p> </td>
  </tr>
 </tbody>
</table>

若要在播放器中設定視訊追蹤：

1. 實例化和設定VisitorAPI程式庫。

       請記住下列資訊：
   
   * 實例化需要由Marketing Cloud提供的Adobe組織ID輸入參數。

      這是字串值。
   * VisitorAPI程式庫的唯一設定選項是後端端點的URL，該URL會提供目前使用者的唯一識別碼。
   * 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。

      如需實作訪客ID服務的相關資訊，請參閱[訪客ID服務實作](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en)。

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. 實例化和設定AppMeasurement元件。

   AppMeasurement例項有許多設定選項。 如需詳細資訊，請前往[Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer)檔案。 下列范常式式碼（`account`、`visitorNamespace`及`trackingServer`）中的選項為必要項目，而值則由Adobe提供。

   >[!IMPORTANT]
   >
   >必須確保已正確設定相依鏈。 AppMeasurement例項匯總（取決於）訪客API元件。

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >在您的應用程式中，請在啟動視訊分析流程之前確認已填入`appMeasurementObject.visitor`，否則可能不會收到任何追蹤結果。 這些結果由日誌中的消息指示。 您可以新增空的追蹤呼叫(`appMeasurementObject.track`)、輪詢`visitor`屬性直到填入為止，然後起始視訊分析。

3. 初始化並設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組中繼，並視需要重新初始化。 重新初始化模組之前，請確定視訊分析中繼資料也更新為正確的內容中繼資料。 要重新建立元資料，請重複子步驟1和2。

   1. 建立Video Analytics中繼資料的例項。
此例項包含啟用視訊心率追蹤所需的所有設定資訊。 例如：

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. 建立媒體播放器例項後，建立Video Analytics追蹤器例項並提供媒體播放器例項的參考。
請記住：

      * 請一律為每個內容播放工作階段建立新的追蹤器例項，並移除先前的參考（分離媒體播放器例項後）。
      * 在子步驟1中建立的中繼資料應提供於Video Analytics追蹤器的建構函式中。

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 銷毀Video Analytics追蹤器。
開始新內容播放工作階段之前，請銷毀視訊追蹤器的先前例項。 收到內容完成事件（或通知）後，請等待幾分鐘再銷毀視訊追蹤器例項。 若立即銷毀例項，可能會干擾Video Analytics追蹤器傳送視訊完成Ping的功能。

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. 手動將即時/線性資料流標示為完成。
如果您的一個即時資料流上有各種集數，可以使用complete API手動將集數標示為已完成。 這會結束目前視訊集數的視訊追蹤工作階段，而您可以開始下一集的新追蹤工作階段。
      >[!TIP]
      >
      >此API為選用API，不是VOD視訊追蹤所需的API。

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
