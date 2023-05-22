---
description: 要testDRM解決方案，您需要一個視頻應用程式，該應用程式可以處理您正在使用的特定DRM解決方案。 此播放器可以是Adobe或您自己的基於TVSDK的視頻應用程式提供的示例播放器。
title: 播放受保護的內容
exl-id: b0e09474-f752-495f-a702-93f288535403
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 播放受保護的內容 {#playback-your-protected-content}

要testDRM解決方案，您需要一個視頻應用程式，該應用程式可以處理您正在使用的特定DRM解決方案。 此播放器可以是Adobe或您自己的基於TVSDK的視頻應用程式提供的示例播放器。

1. 使用從ExpressPlay伺服器返回的令牌響應中的許可證伺服器URL來test是否可以回放受保護的內容。

   * **維德文**  — 直接使用從ExpressPlay許可證令牌請求接收到的Widevine響應。
   * **播放就緒**  — 從許可證令牌請求返回的JSON對象獲取許可證伺服器URL和令牌。
   * **公平遊戲**  — 直接使用從ExpressPlay許可證令牌請求中接收到的FairPlay響應。

1. Test使用您自己的播放器或現有的Adobe樣例播放器播放受保護的內容。

   提供受保護內容的URL（M3U8或MPD清單的位置，具體取決於您正在測試的DRM解決方案）。

   根據與您test的播放器提供的介面，可能會要求您提供許可證URL和標籤，這些URL和標籤分別作為輸入欄位中的字串、貼上到文本框中的JSON對象或URL中的查詢參數。

   下面列出了test球員的一些可能性：

   * HTML5參考播放器：

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * 沙卡玩家：

      ```
      https://shaka-player-demo.appspot.com
      ```

   * TVSDK播放器示例（正在開發中） — 

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **測試FairPlay設定時檢查播放：** 使用ExpressPlay許可證伺服器時，FairPlay需要一些額外步驟來回放內容。 如果您使用 [!DNL curl] test連接（如所述） [許可](../../multi-drm-workflows/quick-start/handle-the-licensing.md))，你需要 *編輯您的M3U8清單* （您的打包內容），如下所示：

1. 將從許可證令牌請求返回的響應添加到 `#EXT-X-KEY:` 清單中的標籤；和
1. 從響應（現在在清單中）、從 `https://` 至 `skd://`。

   下面是用FairPlay測試回放的完整示例，包括許可步驟：

1. 使用FairPlay許可證令牌請求獲取您的許可證令牌URL。 (使用您自己的生產客戶驗證器，並確保使用相同的CEK和 `iv` 用於打包FairPlay內容。) 運行以下命令以獲取示例內容的許可證令牌URL:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   您應該返回一個類似於以下內容的許可證令牌URL的響應：

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 將返回的許可證令牌URL響應放入M3U8清單中， *將許可證令牌URL的方案更改為* `sdk://` 從 `https://`。 以下是M3U8清單中#EXT-X-KEY標籤的示例：

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
   >以上資訊僅適用於FairPlay設定的測試。 它可能不適用於您的生產設定，具體取決於您配置FairPlay處理程式的方式。 請參閱 [在Apple應用程式中啟用FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) 的雙曲餘切值。

如果播放視頻，您已成功打包並授權您的內容。 如果視頻不播放，請查看故障排除頁面以瞭解一些可能的故障解決方案。

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

例如，下面是上面列出的第一個test播放器中的UI部分，您在其中提供了從ExpressPlay伺服器獲取的許可資訊：

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
