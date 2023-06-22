---
description: 您可以設定播放器以追蹤和分析視訊使用情況。
title: 初始化和設定視訊分析
exl-id: dbb1e0b4-2a9e-4687-952d-4772440c1643
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 初始化和設定視訊分析{#initialize-and-configure-video-analytics}

您可以設定播放器以追蹤和分析視訊使用情況。

在啟用視訊追蹤（視訊心率）之前，請確定您具備下列條件：

* 適用於iOS的TVSDK
* 設定/初始化資訊 — 請聯絡您的Adobe代表，取得您的特定視訊追蹤帳戶資訊：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>重要：此JSON設定檔案名稱必須保留 <span class="codeph"> ADBMobileConfig.json </span>. 無法變更此設定檔的名稱和路徑。 此檔案的路徑必須是 <span class="codeph"> &lt;source root=""&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AppMeasurement </span> 追蹤伺服器端點 </td> 
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
   <td colname="col1"> 發佈者 </td> 
   <td colname="col2"> 這是發佈者ID，由客戶的Adobe代表提供給客戶。 <p>提示：此ID不只是一個具有品牌/電視名稱的字串。 </p> </td> 
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

   1. 確認 `ADBMobileConfig.json` 檔案包含Adobe提供的適當值。
   1. 確認此檔案位於 `AdobeMobile` 資料夾。

      此資料夾必須位於應用程式來源樹狀結構的根目錄中。
   1. 編譯及建置您的應用程式。
   1. 部署並執行隨附的應用程式。

      如需這些AppMeasurement設定的詳細資訊，請參閱 [在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).
1. 初始化和設定視訊心率追蹤中繼資料。

   >[!IMPORTANT]
   >
   >您可以停止Video Analytics模組的Midstream，並視需要再次重新初始化。 在重新初始化模組之前，請確定視訊分析中繼資料也已更新為正確的內容中繼資料。 若要重新建立中繼資料，請重複子步驟1和2。

   1. 建立Video Analytics中繼資料的例項。

      此例項包含啟用視訊心率追蹤所需的所有設定資訊。 例如：

      ```
      - (PTVideoAnalyticsTrackingMetadata *)getVideoAnalyticsTrackingMetadata 
      { 
          PTVideoAnalyticsTrackingMetadata *vaTrackingMetadata =  
            [[[PTVideoAnalyticsTrackingMetadata alloc]  
                 initWithTrackingServer:@"example.com" 
                 publisher:@"sample-publisher"] autorelease]; 
      
          // Set these to NO for production deployment. 
          vaTrackingMetadata.debugLogging = YES;  
          vaTrackingMetadata.quietMode = NO; 
      
          vaTrackingMetadata.channel = @"test-channel"; 
          vaTrackingMetadata.videoName = @"myvideo"; 
          vaTrackingMetadata.videoId = @"myvideoid"; 
          vaTrackingMetadata.playerName = @"PSDK Player"; 
          vaTrackingMetadata.enableChapterTracking = YES; 
          vaTrackingMetadata.useSSL = NO; 
          // use this API to override the default asset length -1 for live streams 
          vaTrackingMetadata.assetDuration = SAMPLE_ASSET_DURATION; 
      
      }
      ```

   1. 將Video Analytics中繼資料新增至全域中繼資料例項。

      準備就緒後，請在媒體資源或媒體播放器專案上設定全域中繼資料例項：

      ```
      - (PTMetadata *)createMetadata 
      { 
          PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
      
          [metadata setMetadata:[self getVideoAnalyticsTrackingMetadata]  
            forKey:PTVideoAnalyticsTrackingMetadataKey]; 
      
          return metadata; 
      } 
      
      PTMetadata *metadata = [self createMetadata]; 
      
      PTMediaPlayerItem *item =  
        [[[PTMediaPlayerItem alloc] initWithUrl:[[[NSURL alloc]  
          initWithString:@"media-url"] autorelease] 
          mediaId:@"media-id" metadata:metadata] autorelease];
      ```

   1. 初始化Video Analytics追蹤器

      建立媒體播放器例項後，您必須建立Video Analytics追蹤器例項，並提供媒體播放器例項的參考。

      >[!TIP]
      >
      >請一律為每個內容播放工作階段建立新的追蹤器例項，並在您分離媒體播放器例項後移除先前的參照。

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. 銷毀Video Analytics追蹤器。

      在開始新的內容播放工作階段之前，請先銷毀視訊追蹤器的上一個例項。 收到內容完成事件（或通知）後，請稍候幾分鐘再銷毀視訊追蹤器例項。 立即摧毀執行個體可能會干擾Video Analytics追蹤器傳送視訊完成Ping的功能。

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. 手動將即時/線性資料流標示為完成。

      如果您有一個即時資料流上有各種劇集，可以使用完整的API手動將劇集標示為完成。 如此將結束目前視訊集的視訊追蹤工作階段，而您可以為下一集開始新的追蹤工作階段。

      >[!TIP]
      >
      >此API為選用專案，不需要VOD視訊追蹤。

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```
