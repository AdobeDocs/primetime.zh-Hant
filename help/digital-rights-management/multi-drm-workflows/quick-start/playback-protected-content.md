---
description: 若要測試您的DRM解決方案，您需要一個視訊應用程式，該應用程式可以處理您正在使用的特定DRM解決方案。 此播放器可能是Adobe提供的範例播放器，或是您自己的以TVSDK為基礎的視訊應用程式。
title: 播放您的受保護內容
exl-id: b0e09474-f752-495f-a702-93f288535403
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 播放您的受保護內容 {#playback-your-protected-content}

若要測試您的DRM解決方案，您需要一個視訊應用程式，該應用程式可以處理您正在使用的特定DRM解決方案。 此播放器可能是Adobe提供的範例播放器，或是您自己的以TVSDK為基礎的視訊應用程式。

1. 使用您從ExpressPlay伺服器回傳的權杖回應中的授權伺服器URL，測試您是否可以播放受保護的內容。

   * **Widevine**  — 直接使用從您的ExpressPlay授權Token請求收到的Widevine回應。
   * **PlayReady**  — 從授權權杖請求傳回的JSON物件取得授權伺服器URL和權杖。
   * **Fairplay**  — 直接使用從您的ExpressPlay授權Token請求收到的FairPlay回應。

1. 使用您自己的播放器或現有的Adobe範例播放器，測試受保護內容的播放。

   提供受保護內容的URL （M3U8或MPD資訊清單的位置，視您測試的DRM解決方案而定）。

   根據您測試所用的播放器所提供的介面，系統可能會要求您提供授權URL和權杖，並在輸入欄位中將其分隔為字串、或貼上到文字方塊中的JSON物件，或在URL中將其分隔為查詢引數。

   以下列出測試播放器的一些可能性：

   * HTML5參考播放器：

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player：

      ```
      https://shaka-player-demo.appspot.com
      ```

   * 範例TVSDK播放器（開發中） -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **測試FairPlay設定時檢查播放：** 使用ExpressPlay授權伺服器時，FairPlay需要一些額外的步驟來播放內容。 如果您使用 [!DNL curl] 以測試連線（如所述） [授權](../../multi-drm-workflows/quick-start/handle-the-licensing.md))，您需要 *編輯您的M3U8資訊清單* （您的封裝內容）如下所示：

1. 將授權權杖請求傳回的回應新增至 `#EXT-X-KEY:` 標籤進行標籤；及
1. 從回應（現在在資訊清單中）變更該URL的通訊協定，從 `https://` 至 `skd://`.

   以下是使用FairPlay測試播放的完整範例，包括授權步驟：

1. 使用FairPlay授權權杖請求來取得您的授權權杖URL。 (使用您自己的生產客戶驗證器，並確保使用相同的CEK和 `iv` 用來封裝您的FairPlay內容)。 執行以下命令以取得範例內容的授權權杖URL：

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   您應該會以授權權杖URL得到回應，如下所示：

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 將傳回的授權權杖URL回應放入您的M3U8資訊清單，並且 *將授權權杖URL的方案變更為* `sdk://` 從 `https://`. 以下是M3U8資訊清單中#EXT-X-KEY標籤的範例：

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
   >上述資訊僅適用於FairPlay設定的測試。 它可能不適用於您的生產設定，具體取決於您設定FairPlay處理常式的方式。 另請參閱 [在iOS應用程式中啟用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) 以取得詳細資訊。

如果您的影片播放，表示您已成功封裝並授權您的內容。 如果影片無法播放，請前往疑難排解頁面，尋找問題的可能解決方案。

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

例如，以下是上述第一個測試播放器中的UI部分，您可在其中提供從ExpressPlay伺服器取得的授權資訊：

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
