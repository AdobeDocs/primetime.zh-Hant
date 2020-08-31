---
description: 'null'
seo-description: 'null'
seo-title: 初始化和設定視訊分析
title: 初始化和設定視訊分析
uuid: 98017a20-4997-42f7-9b03-fd9c4b6ccd92
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# 初始化和設定視訊分析 {#initialize-and-configure-video-analytics}

您可以設定您的播放器來追蹤和分析視訊使用。
在啟動視訊追蹤（視訊心率）之前，請確定您有下列項目：

* Android專用的TVSDK 2.5。
* 配置／初始化資訊

   請連絡您的Adobe代表，以取得您的特定視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>重要： 此JSON設定檔案名稱必須保 <span class="filepath"> 留為ADBMobileConfig.json </span>。 無法更改此配置檔案的名稱和路徑。 此檔案的路徑必須 <span class="filepath"> 是&lt;source root&gt;/assets </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement追蹤伺服器端點 </td> 
   <td colname="col2"> Adobe Analytics（舊稱SiteCatalyst）後端收集端點的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 視訊分析追蹤伺服器端點 </td> 
   <td colname="col2"> 視訊分析後端收集端點的URL。 這是傳送所有視訊心率追蹤呼叫的地方。 <p>提示： 訪客追蹤伺服器的URL與分析追蹤伺服器的URL相同。 如需實作訪客ID服務的詳細資訊，請參閱實 <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> 作ID服務 </a>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帳戶名稱 </td> 
   <td colname="col2"> 也稱為報表套裝ID(RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud組織ID </td> 
   <td colname="col2"> 執行個體化訪客元件所需的字串值。 </td> 
  </tr> 
 </tbody> 
</table>

若要在您的播放器中設定視訊追蹤：

1. 確認資源檔案中的載入時 `ADBMobileConfig.json` 間選項正確。

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

   此JSON格式的設定檔會與TVSDK搭售為資源。 您的播放器只會在載入時讀取這些值，而且當您的應用程式執行時，這些值會維持不變。

   要配置載入時間選項：


   1. 確認檔 `ADBMobileConfig.json` 案包含適當的值（由Adobe提供）。
   1. 確認此檔案位於資料夾 `assets/` 中。

      此資料夾必須位於應用程式源樹的根目錄中。

   1. 編譯並建立您的應用程式。
   1. 部署並執行整合的應用程式。

      如需這些AppMeasurement設定的詳細資訊，請參 [閱「在Adobe Analytics中測量視訊」](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/)。

1. 初始化並設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止視訊分析模組中間串流，並視需要重新初始化它。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複下列前兩個步驟(子 **步驟** a **和b**)。

   1. 建立視訊分析中繼資料的例項。

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

   1. 初始化視訊分析提供者。

      建立媒體播放器例項後，您必須建立視訊分析提供者例項，並提供應用程式內容給該例項。

      >[!TIP]
      >
      >請務必為每個內容播放作業建立新的提供者例項，並在分離媒體播放器例項後移除先前的參考。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. 在例項上設定視訊分析中繼 `videoAnalyticsProvider` 資料。

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. 將媒體播放器例項附加至例 `videoAnalyticsProvider` 項：

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 銷毀視訊分析提供者。

      開始新的內容播放作業前，請銷毀視訊提供者的先前例項。 收到內容完成事件（或通知）後，請等候幾分鐘，再銷毀視訊分析提供者例項。 立即銷毀執行個體可能會干擾視訊分析提供者傳送「視訊完成」ping的能力。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. 手動將即時／線性串流標示為完成。

      如果您在一個即時串流上有不同的集數，您可以使用完整的API手動將集數標示為完整。 這會結束目前視訊集的視訊追蹤工作階段，而您可以開始下一集的新追蹤工作階段。

      >[!TIP]
      >
      >此API為選用API，無法用於VOD視訊追蹤。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

