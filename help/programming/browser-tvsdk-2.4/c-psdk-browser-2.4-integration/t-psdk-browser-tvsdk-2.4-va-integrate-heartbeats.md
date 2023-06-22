---
description: 您可以設定播放器以追蹤和分析視訊使用情況。
title: 初始化和設定視訊分析
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 初始化和設定視訊分析 {#initialize-and-configure-video-analytics}

您可以設定播放器以追蹤和分析視訊使用情況。

在啟用視訊追蹤（視訊心率）之前，請確定您具備下列條件：

* 設定/瀏覽器TVSDK初始化資訊 — 請聯絡您的Adobe代表，取得您的特定視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
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
  <tr>
   <td colname="col1"> 訪客追蹤伺服器端點 </td>
   <td colname="col2"> 為目前視訊檢視器提供唯一識別碼的後端端點URL。 </td>
  </tr>
  <tr>
   <td colname="col1"> 發佈者 </td>
   <td colname="col2"> 這是發佈者ID，由客戶的Adobe代表提供給客戶。 <p>提示：此ID不只是一個具有品牌/電視名稱的字串。 </p> </td>
  </tr>
 </tbody>
</table>

若要在播放器中設定視訊追蹤：

1. 例項化及設定VisitorAPI程式庫。

       請記住下列資訊：
   
   * 具現化需要Adobe提供的Marketing Cloud組織ID輸入引數。

      這是字串值。
   * VisitorAPI程式庫唯一的設定選項是後端端點的URL，可提供目前使用者的唯一識別碼。
   * 訪客追蹤伺服器的URL與Analytics追蹤伺服器的URL相同。

      如需實作訪客ID服務的相關資訊，請參閱 [訪客ID服務實作](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. 例項化及設定AppMeasurement元件。

   AppMeasurement例項有許多設定選項。 如需詳細資訊，請前往 [Adobe Analytics開發人員](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 說明檔案。 下列範常式式碼中的選項( `account`， `visitorNamespace`、和 `trackingServer`)為必填欄位，而值是由Adobe提供。

   >[!IMPORTANT]
   >
   >您必須確保相依性鏈已正確設定。 AppMeasurement例項會彙總（取決於）訪客API元件。

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
   >在您的應用程式中，確認 `appMeasurementObject.visitor` 會在起始video analytics流程之前填入，否則您可能得不到任何追蹤結果。 記錄中的訊息會指出這些結果。 您可以新增空白追蹤呼叫( `appMeasurementObject.track`)，輪詢 `visitor` 屬性，直到填入為止，並啟動視訊分析。

3. 初始化和設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止Video Analytics模組的Midstream，並視需要再次重新初始化。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複子步驟1和2。

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

   2. 建立媒體播放器例項後，請建立Video Analytics追蹤器例項，並提供該媒體播放器例項的參考。
請記住以下事項：

      * 請一律為每個內容播放工作階段建立新的追蹤器例項，並移除先前的參照（在分離媒體播放器例項後）。
      * 在子步驟1中建立的中繼資料應提供在Video Analytics追蹤器的建構函式中。

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 銷毀Video Analytics追蹤器。
在開始新的內容播放工作階段之前，請先銷毀視訊追蹤器的上一個例項。 收到內容完成事件（或通知）後，請稍候幾分鐘再銷毀視訊追蹤器例項。 立即摧毀執行個體可能會干擾Video Analytics追蹤器傳送視訊完成Ping的功能。

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. 手動將即時/線性資料流標示為完成。
如果您有一個即時資料流上有各種劇集，可以使用完整的API手動將劇集標示為完成。 如此將結束目前視訊集的視訊追蹤工作階段，而您可以為下一集開始新的追蹤工作階段。
      >[!TIP]
      >
      >此API為選用專案，不需要VOD視訊追蹤。

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
