---
description: 您可以配置播放器以跟蹤和分析視頻使用。
title: 初始化和配置視頻分析
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# 初始化和配置視頻分析 {#initialize-and-configure-video-analytics}

您可以配置播放器以跟蹤和分析視頻使用。

在激活視頻跟蹤（視頻心跳）之前，請確保您有以下幾點：

* 配置/瀏覽器TVSDK初始化資訊 — 有關特定視頻跟蹤帳戶資訊，請與Adobe代表聯繫：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
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
   <td colname="col1"> 訪問者跟蹤伺服器端點 </td>
   <td colname="col2"> 為當前視頻查看器提供唯一標識符的後端終結點的URL。 </td>
  </tr>
  <tr>
   <td colname="col1"> 發佈者 </td>
   <td colname="col2"> 這是發佈者ID，由客戶的Adobe代表提供給客戶。 <p>提示：此ID不僅是帶有品牌/電視名稱的字串。 </p> </td>
  </tr>
 </tbody>
</table>

要在播放器中配置視頻跟蹤，請執行以下操作：

1. 實例化並配置VisitorAPI庫。

       請牢記以下資訊：
   
   * 實例化需要由Marketing Cloud提供的Adobe組織ID輸入參數。

      這是字串值。
   * VisitorAPI庫的唯一配置選項是提供當前用戶的唯一標識符的後端終結點的URL。
   * 訪問者跟蹤伺服器的URL與分析跟蹤伺服器的URL相同。

      有關實施訪問者ID服務的資訊，請參見 [訪問者ID服務實施](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en)。

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. 實例化並配置AppMeasurement元件。

   AppMeasurement實例具有許多配置選項。 有關詳細資訊，請轉至 [Adobe Analytics開發商](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 文檔。 以下示例代碼中的選項( `account`。 `visitorNamespace`, `trackingServer`)，這些值由Adobe提供。

   >[!IMPORTANT]
   >
   >必須確保正確設定依賴關係鏈。 AppMeasurement實例聚合（取決於）訪問者API元件。

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
   >在您的應用程式中，確保 `appMeasurementObject.visitor` 在啟動視頻分析流之前填充，或者您可能沒有得到任何跟蹤結果。 這些結果由日誌中的消息指示。 可以添加空磁軌調用( `appMeasurementObject.track`)，輪詢 `visitor` 屬性，然後啟動視頻分析。

3. 初始化和配置視頻心跳跟蹤元資料。

   >[!IMPORTANT]
   >
   >您可以停止視頻分析模組中流，並根據需要重新初始化它。 在重新初始化模組之前，請確保視頻分析元資料也更新為正確的內容元資料。 要重新建立元資料，請重複子步驟1和2。

   1. 建立視頻分析元資料的實例。
此實例包含啟用視頻心跳跟蹤所需的所有配置資訊。 例如：

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

   2. 建立媒體播放器實例後，建立視頻分析跟蹤器實例並提供對媒體播放器實例的引用。
請記住以下內容：

      * 始終為每個內容播放會話建立新的跟蹤器實例，並刪除以前的引用（在分離媒體播放器實例後）。
      * 在子步驟1中建立的元資料應在視頻分析跟蹤器的建構子中提供。

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 銷毀視頻分析跟蹤器。
在開始新的內容播放會話之前，請銷毀視頻跟蹤器的先前實例。 收到內容完成事件（或通知）後，請等待幾分鐘，然後銷毀視頻跟蹤器實例。 立即銷毀實例可能會干擾視頻分析跟蹤程式發送視頻完成ping的能力。

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. 手動將Live/Linear流標籤為完成。
如果您在一個即時流上有各種集數，則可以使用完整的API手動將集數標籤為完整。 這將結束當前視頻集的視頻跟蹤會話，並且您可以為下一集啟動新的跟蹤會話。
      >[!TIP]
      >
      >此API是可選的，不需要用於VOD視頻跟蹤。

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
