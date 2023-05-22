---
description: DRM工作流涉及打包您的內容、為內容提供許可，以及從您自己的視頻應用程式中回放受保護的內容。 對於每個DRM解決方案，工作流通常都相似，但在細節方面有一些不同。
title: FairPlay的多DRM工作流
exl-id: a66cecda-762b-48f7-afed-6fef6303d169
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# FairPlay的多DRM工作流 {#multi-drm-workflow-for-fairplay}

DRM工作流涉及打包您的內容、為內容提供許可，以及從您自己的視頻應用程式中回放受保護的內容。 對於每個DRM解決方案，工作流通常都相似，但在細節方面有一些不同。

此多DRM工作流將帶您完成使用AppleFairPlay保護的HLS內容的設定、打包、許可和回放。 此工作流還包含用於實現離線播放和許可證輪換的可選說明。

## 為FairPlay啟用ExpressPlay服務 {#enable-expressplay-service-for-fairplay}

Apple的FairPlay DRM解決方案在與ExpressPlay DRM服務一起使用時需要進行一些設定。 這包括從Apple獲取憑據並將其上傳到ExpressPlay。

按照以下步驟啟用ExpressPlay服務以保護FairPlay內容。

1. 從Apple獲得證書。

   這些憑據被唯一地設定給每個服務提供商。 您必須通過填寫以下表單來請求： [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/)。

   >[!NOTE]
   >
   >選擇 **[!UICONTROL Content Provider]** 。

   一旦你的請求獲得批准，Apple會 *FairPlay流式部署包*。
1. 生成證書籤名請求。

   您可以使用 [!DNL openssl] 生成公用/私鑰對和證書籤名請求(CSR)。

   1. 生成密鑰對。

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. 生成CSR。

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >此步驟的說明位於 *FairPlay流式部署包*，但為方便起見，請在此提供。 如果您對此部分流程有問題，請查看 *FairPlayCertificateCreation.pdf* （在部署包中）。

1. 通過Apple開發人員門戶上傳您的CSR。
   1. 開發團隊的團隊代理必須登錄 [!DNL developer.apple.com/account]。
   1. 按一下 **[!UICONTROL Certificates, Identifiers & Profiles]**，然後選擇 **[!UICONTROL iOS, tvOS, watchOS]** 下拉到頁面左上角，然後按一下 **[!UICONTROL Certificates->Production]** 頁左側。
   1. 按一下 **[!UICONTROL +]** 的子菜單。 選擇 **[!UICONTROL FairPlay Streaming Certificate]** 選項 **[!UICONTROL Production]**。

      的 *添加iOS證書* 對話框。
   1. 在 *添加iOS證書*&#x200B;上載在步驟2.b中生成的CSR檔案，然後按一下 **[!UICONTROL Generate]**。

      您的應用程式密鑰(ASK)顯示在同一對話框中。
   1. 記下您的ASK，並將其儲存在安全位置。
   1. ASK中的密鑰以完成證書生成，然後按一下 **[!UICONTROL Continue]**。
   1. 驗證是否已保存ASK後，按一下 **[!UICONTROL Generate]** 繼續。

      >[!NOTE]
      >
      >保存ASK副本並安全地儲存它非常重要。 *如果您的ASK受到損害，您將無法再通過FairPlay流式處理保護您的內容。* 只有一(1)個ASK分配給您的團隊。 將不再提供該值，您以後無法檢索它。

   1. 下載FPS證書。

      確保將私鑰（從步驟2.a.）和公鑰（在此步驟中下載的FPS證書）的備份副本保存在安全位置。
1. 使用FairPlay憑據設定ExpressPlay帳戶。
   1. 假設您在步驟3.h中下載的證書名稱。是 [!DNL fairplay.cer]。
   1. 開啟 [!DNL fairplay.cer] 檔案。
   1. 通過輸入「」篩選您的許多證書 `fairplay`」對話框。
   1. 確定您公司的FairPlay證書。

      您的公司名稱應與Apple頒發的證書關聯。
   1. 通過選擇展開箭頭展開證書，然後按一下右鍵您的私鑰。
   1. 選擇 **[!UICONTROL Export "Your Company Name"]** 並保存 [!DNL .p12] 的子菜單。

      將要求您分配密碼以保護此檔案。 記下此密碼，因為您需要將此密碼與您的憑據包一起發送。
   1. 登錄帳戶 [www.expressplay.com](https://www.expressplay.com)。
   1. 按一下 **[!UICONTROL DRM SERVICES]** 在左上角，選擇 **[!UICONTROL FairPlay]** 頁籤。
   1. 將FairPlay憑據上載到ExpressPlay帳戶。

      1. 建立包含ASK值的文本檔案(應為32個字元，例如： `1234567890abcdef1234567890abcdef`)，並選擇此檔案進行上載。
      1. 從步驟4.f中選擇PKCS12檔案。上載。
      1. 在步驟4.f中輸入PKCS12檔案密碼。
      1. 按一下「Upload（上載）」按鈕。

現在，您可以建立iOS應用程式或HTML5頁，同時提供FairPlay內容保護 [!DNL fairplay.cer] 使用ExpressPlay服務的證書。

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### 將您的內容打包以用於FairPlay {#package-your-content-for-fairplay}

要打包內容，您可以使用Adobe離線打包程式或其他工具，如ExpressPlay的Bento4打包程式。

打包員準備視頻以進行回放（例如，將原始檔案分片並放入清單），並使用您選擇的DRM解決方案（在本例中為FairPlay）保護視頻：

* [AdobeFairPlay DRM離線打包器](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay打包器 — HLS的Bento4](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 打包您的內容。

   下面是使用Adobe離線打包器的打包示例。 打包器使用配置檔案(例如， [!DNL fairplay.xml])，它看起來是這樣的：

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path`  — 此入口指向本地打包機上源視頻的位置。
   * `out_type`  — 此條目描述打包輸出的類型，在本例中為FairPlay的HLS。
   * `out_path`  — 希望輸出到的本地電腦上的位置。
   * `drm_sys`  — 要打包的DRM解決方案。 這是 `FAIRPLAY` 在這個例子中。
   * `frag_dur`  — 片段持續時間（秒）。
   * `target_dur` - HLS輸出的目標持續時間。
   * `key_file_path`  — 這是作為內容加密密鑰(CEK)的打包電腦上許可證檔案的位置。 它是Base-64編碼的16位元組十六進位字串。
   * `iv_file_path`  — 這是包裝機上IV檔案的位置。
   * `key_url`  — 的URI參數 `EXT-X-KEY` 標籤 [!DNL .m3u8] 的子菜單。
   * `content_id`  — 預設值。

   如 [打包程式文檔](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)，「作為最佳做法，建立包含要用於生成輸出的常用選項的配置檔案。 然後，通過提供特定選項作為命令行參數來建立輸出。」

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   生成的M3U8檔案 `EXT-X-KEY` 屬性，如下所示：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### 設定FairPlay的策略 {#setting-policies-for-fairplay}

可以使用權利伺服器為受公平播放保護的內容設定策略。 您可以設定自己的權限，或使用Adobe提供的示例權限伺服器。

Adobe提供一個示例ExpressPlay權利伺服器(SEES)，該伺服器顯示如何 *基於時間* 和 *設備綁定* 權利。 此示例權利伺服器構建在ExpressPlay服務之上。

[參考伺服器：示例ExpressPlay權利伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [參考服務：基於時間的權利](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [參考服務：設備綁定權利](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay的許可和播放 {#licensing-and-playback-for-fairplay}

授權和播放受公平播放保護的內容需要在視頻清單檔案(skd:)中使用的方案和ExpressPlay令牌請求(https:)中使用的方案之間交換URL方案。

從iOSTVSDK客戶端實現許可和播放的說明如下： [在TVSDK應用程式中啟用Apple公平播放](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)。 您還可以選擇為FairPlay實現離線播放和許可證輪換。

## HLS FairPlay離線 {#section_047A05D1E3B64883858BC601CFC8F759}

當無法檢索到受公平播放保護的內容時，您可能希望用戶能夠播放該內容，因為該播放器與網頁（如在飛機上）隔離。

開始此任務之前，請下載並閱讀Apple文檔 **「Offline Playback with FairPlay Streaming and HTTP Live Streaming」**。 閱讀指南，瞭解如何下載傳輸流(TS)段並將其保存到本地電腦。

通過此工作流為FairPlay實施離線播放：

1. 下載HLS TS段。
1. 從FairPlay伺服器請求永久租用許可證（請參見） **&quot;FairPlay持續租賃政策&quot;**)。
1. 保存 `persistentContentKey`。
1. 離線播放FairPlay內容。

>[!NOTE]
>
>如果保留的內容密鑰已過期，客戶端上的FairPlay流不會啟動解密。 但是，如果內容密鑰在回放期間過期，則它將繼續用戶體驗。
>
>請參閱 [使用HTTP即時流](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) 的子菜單。

### 公平播放許可證輪換 {#section_D32AA08C61474B4F876AC2A5F18CB879}

許可證輪換是防止長期播放內容的許可證駭客的方案。

在M3U8清單中，每個密鑰標籤將應用於以下TS段，直到下一個密鑰標籤或檔案結束。

要添加許可證輪替，請執行以下操作：

* 在許可證輪換期間插入新的FairPlay密鑰標籤。

   可以添加任意數量的密鑰標籤。

   對於線性內容，請確保在M3U8窗口中維護最新的密鑰標籤。 iOS將請求下一個M3U8，當剩餘大約兩個TS段要播放時（大約20秒）。 如果新M3U8包含新密鑰標籤，則所有密鑰請求都將立即發生。 將不再請求以前的現有密鑰。 iOS將等待所有關鍵請求完成，然後再開始播放。

   對於具有許可證循環的VOD內容，所有關鍵請求都將在播放開始時發生。

   以下是帶鍵旋轉的示例M3U8:

   ```
   #EXTM3U
   #EXT-X-TARGETDURATION:10
   #EXT-X-VERSION:5
   #EXT-X-MEDIA-SEQUENCE:0
   #EXT-X-PLAYLIST-TYPE:VOD
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
   212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence0.ts
   #EXTINF:10,
   fileSequence1.ts
   #EXTINF:10,
   fileSequence2.ts
   #EXTINF:10,
   fileSequence3.ts
   #EXTINF:10,
   fileSequence4.ts
   #EXTINF:10,
   fileSequence5.ts
   #EXTINF:10,
   fileSequence6.ts
   #EXTINF:10,
   fileSequence7.ts
   #EXTINF:10,
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
   337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
   keydelivery",KEYFORMATVERSIONS="1"
   #EXTINF:10,
   fileSequence8.ts
   #EXTINF:10,
   ```
