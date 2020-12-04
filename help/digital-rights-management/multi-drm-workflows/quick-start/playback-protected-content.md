---
description: 要測試您的DRM解決方案，您需要一個視頻應用程式，它可以處理您正在使用的特定DRM解決方案。 此播放器可以是Adobe提供的範例播放器，或您自己的TVSDK視訊應用程式。
seo-description: 要測試您的DRM解決方案，您需要一個視頻應用程式，它可以處理您正在使用的特定DRM解決方案。 此播放器可以是Adobe提供的範例播放器，或您自己的TVSDK視訊應用程式。
seo-title: 播放您的受保護內容
title: 播放您的受保護內容
uuid: 84f73ee7-43d0-481c-a5e7-14f92169323c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# 播放受保護的內容{#playback-your-protected-content}

要測試您的DRM解決方案，您需要一個視頻應用程式，它可以處理您正在使用的特定DRM解決方案。 此播放器可以是Adobe提供的範例播放器，或您自己的TVSDK視訊應用程式。

1. 從ExpressPlay伺服器傳回的代號回應使用授權伺服器URL，以測試您是否可以播放受保護的內容。

   * **Widevine**  —— 直接從您的ExpressPlay授權Token要求接收到Widevine回應。
   * **PlayReady** -從您的授權Token請求傳回的JSON物件取得授權伺服器URL和Token。
   * **FairPlay**  —— 直接從您的ExpressPlay授權Token要求接收到FairPlay回應。

1. 使用您自己的播放器或現有的Adobe範例播放器，測試受保護內容的播放。

   提供您受保護內容的URL（M3U8或MPD資訊清單的位置，視您正在測試的DRM解決方案而定）。

   視您所測試的播放器提供的介面而定，可能會要求您在輸入欄位中個別提供授權URL和Token作為字串，或是貼入文字方塊中的JSON物件，或是當做URL中的查詢參數。

   以下列出測試播放器的一些可能性：

   * HTML5參考播放器：

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * 範例TVSDK播放器（開發中）-

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **在測試FairPlay設定時檢查播放：** FairPlay在使用ExpressPlay授權伺服器時，需要額外的步驟來播放內容。如果您使用[!DNL curl]來測試連線（如[Licensing](../../multi-drm-workflows/quick-start/handle-the-licensing.md)所述），則需要&#x200B;*編輯您的M3U8 manifest*（您的封裝內容），如下所示：

1. 將您從授權Token要求中收到的回應新增至資訊清單中的`#EXT-X-KEY:`標籤；和
1. 將該URL的通訊協定從回應（現在位於資訊清單中）從`https://`變更為`skd://`。

   以下是使用FairPlay測試播放的完整範例，包括授權步驟：

1. 使用FairPlay授權Token請求以取得您的授權Token URL。 （請使用您自己的「生產客戶驗證器」，並務必使用用來封裝FairPlay內容的相同CEK和`iv`。） 執行下列命令以取得範例內容的授權Token URL:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   您應該會收到回覆，其中包含類似下列的授權Token URL:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 將傳回的授權Token URL回應放入您的M3U8資訊清單中，並&#x200B;*將授權Token URL的配置從`https://`變更為* `sdk://`。 以下是M3U8資訊清單中#EXT-X-KEY標籤的範例：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >上述資訊僅適用於FairPlay設定的測試。 視您設定FairPlay處理常式的方式而定，它可能不適用於您的生產設定。 如需詳細資訊，請參閱[在iOS應用程式中啟用Apple FairPlay。](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

如果您的視訊播放，您已成功封裝並授權您的內容。 如果您的視訊無法播放，請查看疑難排解頁面，以取得一些解決問題的可能方案。

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

例如，上列第一個測試播放器的UI部分，您可在其中提供從ExpressPlay伺服器取得的授權資訊：

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
