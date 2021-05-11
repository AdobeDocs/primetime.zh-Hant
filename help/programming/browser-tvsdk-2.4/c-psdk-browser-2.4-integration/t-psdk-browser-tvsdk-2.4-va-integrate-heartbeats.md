---
description: 您可以設定您的播放器來追蹤和分析視訊使用。
title: 初始化和設定視訊分析
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
translation-type: tm+mt
source-git-commit: d884836a2a585bd3540b085de1098cf6ae3de46b
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# 初始化並設定視訊分析{#initialize-and-configure-video-analytics}

您可以設定您的播放器來追蹤和分析視訊使用。

在啟動視訊追蹤（視訊心率）之前，請確定您有下列項目：

* 設定／瀏覽器TVSDK初始化資訊——請連絡您的Adobe代表，以取得特定視訊追蹤帳戶資訊：

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

      如需實作訪客ID服務的詳細資訊，請參閱[訪客ID服務實作](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html)。

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. 執行個體化及設定AppMeasurement元件。

   AppMeasurement例項有許多設定選項。 如需詳細資訊，請至[Adobe Analytics開發人員](https://microsite.omniture.com/t2/help/en_US/reference/#Developer)檔案。 下列范常式式碼（`account`、`visitorNamespace`和`trackingServer`）中的選項為必要項，而值則由Adobe提供。

   >[!IMPORTANT]
   >
   >必須確保已正確設定從屬關係鏈。 AppMeasurement例項會匯總（視訪客API元件而定）。

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
   >在您的應用程式中，請確定在開始視訊分析流程之前已填入`appMeasurementObject.visitor`，否則可能無法取得任何追蹤結果。 這些結果由日誌中的消息指示。 您可以新增空的追蹤呼叫(`appMeasurementObject.track`)、輪詢`visitor`屬性，直到填入為止，並啟動視訊分析。

3. 初始化並設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組中間串流，並視需要重新初始化它。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複子步驟1和2。

   1. 建立視訊分析中繼資料的例項。
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

   2. 建立媒體播放器例項後，請建立視訊分析追蹤器例項並提供媒體播放器例項的參考。
請記住：

      * 請務必為每個內容播放作業建立新的追蹤器例項，並移除先前的參考（在分離媒體播放器例項後）。
      * 在子步驟1中建立的中繼資料應提供在視訊分析追蹤器的建構函式中。

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 銷毀視訊分析追蹤器。
開始新的內容播放作業前，請先銷毀視訊追蹤器的先前例項。 收到內容完成事件（或通知）後，請等候幾分鐘，再銷毀視訊追蹤器例項。 立即銷毀執行個體可能會干擾視訊分析追蹤器傳送視訊完成ping的功能。

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. 手動將即時／線性串流標示為完成。
如果您在一個即時串流上有不同的集數，您可以使用完整的API手動將集數標示為完整。 這會結束目前視訊集的視訊追蹤工作階段，而您可以開始下一集的新追蹤工作階段。
      >[!TIP]
      >
      >此API為選用API，不需要用於VOD視訊追蹤。

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
