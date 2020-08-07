---
description: DRM工作流程包括封裝您的內容、提供內容授權，以及從您自己的視訊應用程式中播放受保護的內容。 每個DRM解決方案的工作流程通常都很相似，但細節方面有一些不同。
seo-description: DRM工作流程包括封裝您的內容、提供內容授權，以及從您自己的視訊應用程式中播放受保護的內容。 每個DRM解決方案的工作流程通常都很相似，但細節方面有一些不同。
seo-title: FairPlay的多DRM工作流程
title: FairPlay的多DRM工作流程
uuid: cd940a70-400c-435e-8322-55bd624164e1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---


# FairPlay的多DRM工作流程 {#multi-drm-workflow-for-fairplay}

DRM工作流程包括封裝您的內容、提供內容授權，以及從您自己的視訊應用程式中播放受保護的內容。 每個DRM解決方案的工作流程通常都很相似，但細節方面有一些不同。

此多DRM工作流程可引導您完成使用Apple FairPlay保護的HLS內容的設定、封裝、授權和播放。 此工作流程也包含實作離線播放和授權旋轉的選用指示。

## 為FairPlay啟用ExpressPlay服務 {#enable-expressplay-service-for-fairplay}

Apple的FairPlay DRM解決方案在您搭配ExpressPlay DRM服務使用時，需要進行一些設定。 這包括從Apple取得認證，並將認證上傳至ExpressPlay。

請依照下列步驟，啟用ExpressPlay服務以保護FairPlay內容。

1. 從Apple取得認證。

   這些認證是唯一提供給每個服務提供者的。 您必須填妥下清單格，以索取： [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >選擇 **[!UICONTROL Content Provider]** 主要角色。

   在您的要求獲得核准後，Apple會傳送 *FairPlay串流部署套件給您*。
1. 產生憑證簽署要求。

   您可以使 [!DNL openssl] 用來產生公用／私用金鑰對，以及您的憑證簽署請求(CSR)。

   1. 產生您的金鑰對。

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. 產生您的CSR。

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >此步驟的說明位於您的 *FairPlay串流部署套件中*，但為方便您，此處提供。 如果您對此程式部分有任何問題，請查看 *FairPlayCertificateCreation.pdf* （在您的部署套件中）中的指示。

1. 透過Apple開發人員入口網站上傳您的CSR。
   1. 您的開發團隊的團隊代理必須登入 [!DNL developer.apple.com/account]。
   1. 按一 **[!UICONTROL Certificates, Identifiers & Profiles]**&#x200B;下，然後選 **[!UICONTROL iOS, tvOS, watchOS]** 取頁面左上方的下拉式清單，然後按 **[!UICONTROL Certificates->Production]** 一下頁面左側的。
   1. 按一 **[!UICONTROL +]** 下頁面右上角的按鈕以請求新憑證。 選擇下 **[!UICONTROL FairPlay Streaming Certificate]** 面的選項 **[!UICONTROL Production]**。

      隨即 *開啟「新增iOS憑證* 」對話方塊。
   1. 在「新 *增iOS憑證*」中，上傳您在步驟2.b.中產生的CSR檔案，然後按一下 **[!UICONTROL Generate]**。

      您的應用程式密鑰(ASK)會顯示在相同的對話方塊中。
   1. 記下您的ASK，並將它儲存在安全的位置。
   1. ASK中的金鑰以完成憑證產生，然後按一下 **[!UICONTROL Continue]**。
   1. 確認已保存ASK後，按一下繼 **[!UICONTROL Generate]** 續。

      >[!NOTE]
      >
      >請務必儲存ASK的副本並安全地儲存。 *如果您的ASK受到危害，您將無法再使用FairPlay串流保護您的內容。* 您的團隊只有一(1)個ASK。 將不再提供該值，您以後也無法檢索它。

   1. 下載您的FPS憑證。

      請務必將私密金鑰（來自步驟2.a.）和公開金鑰（您在此步驟中下載的FPS憑證）的備份副本儲存在安全的位置。
1. 使用您的FairPlay認證來設定您的ExpressPlay帳戶。
   1. 假設您在步驟3.h中下載的憑證名稱。的 [!DNL fairplay.cer]值。
   1. 使用Apple [!DNL fairplay.cer] Keychain Access公用程式開啟檔案。
   1. 在右上角的搜尋欄位中輸 `fairplay`入「」，以篩選您的許多憑證。
   1. 識別您公司的FairPlay憑證。

      您的公司名稱應與Apple核發的憑證相關聯。
   1. 選擇展開箭頭以展開憑證，然後在私密金鑰上按一下滑鼠右鍵。
   1. 選擇 **[!UICONTROL Export "Your Company Name"]** 並保存文 [!DNL .p12] 件。

      系統會要求您指定密碼以保護此檔案。 請記下此密碼，因為您需要將此密碼與您的認證套件一起傳送。
   1. 請登入您的帳戶( [www.expressplay.com](https://www.expressplay.com))。
   1. 按一 **[!UICONTROL DRM SERVICES]** 下左上角的，然後選取標 **[!UICONTROL FairPlay]** 簽。
   1. 將您的FairPlay認證上傳至您的ExpressPlay帳戶。

      1. 建立包含ASK值的文字檔案(例如： `1234567890abcdef1234567890abcdef`)，並選取此檔案進行上傳。
      1. 從步驟4.f中選擇PKCS12檔案。上傳。
      1. 在步驟4.f中輸入PKCS12檔案口令。
      1. 按一下「上傳」按鈕。

現在，您可以使用FairPlay專用的ExpressPlay服務，建立具有FairPlay內容保護的iOS應用程式或HTML5 [!DNL fairplay.cer] 網頁以及您的憑證。

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### 將您的內容封裝為FairPlay {#package-your-content-for-fairplay}

若要封裝內容，您可以使用Adobe Offline Packager或其他工具，例如ExpressPlay的Bento4封裝程式。

封裝程式會準備視訊以供播放（例如，將原始檔案分割並放入資訊清單中），並使用您選擇的DRM解決方案保護視訊（在此例中為FairPlay）:

* [Adobe Offline Packager for FairPlay DRM](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay Packagers - Bento4 for HLS](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 封裝您的內容。

   以下是使用Adobe Offline Packager的封裝範例。 Packager使用配置檔案(例如 [!DNL fairplay.xml])，其外觀類似：

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

   * `in_path` -此入口指向您本機封裝機器上來源視訊的位置。
   * `out_type` -此條目描述了打包輸出的類型，在本例中為HLS for FairPlay。
   * `out_path` -您希望輸出移至本機電腦的位置。
   * `drm_sys` -您要封裝的DRM解決方案。 這就 `FAIRPLAY` 是這個。
   * `frag_dur` -片段持續時間（秒）。
   * `target_dur` - HLS輸出的目標持續時間。
   * `key_file_path` -此為授權檔案在包裝機器上的位置，用作您的內容加密金鑰(CEK)。 它是Base-64編碼的16位元組十六進位字串。
   * `iv_file_path` -這是包裝機上IV檔案的位置。
   * `key_url` -檔案標籤的 `EXT-X-KEY` URI參 [!DNL .m3u8] 數。
   * `content_id` -預設值。

   如 [Packager檔案所述](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7),「最佳實務是，建立組態檔，其中包含您要用來產生輸出的常用選項。 然後，通過提供特定選項作為命令行參數來建立輸出。」

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   產生的M3U8檔案有一 `EXT-X-KEY` 個屬性，如下所示：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### 設定FairPlay的政策 {#setting-policies-for-fairplay}

您可以使用權益伺服器來設定受FairPlay保護內容的政策。 您可以設定自己的權益，或使用Adobe提供的範例權益伺服器。

Adobe提供範例ExpressPlay Entitlement Server(SEES)，可顯示如何執行 *時間型**和裝置系結權益* 。 此範例權益伺服器是以ExpressPlay服務為基礎。

[參考伺服器：範例ExpressPlay Entitlement Server(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [參考服務：時間型權益](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [參考服務：裝置系結權益](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay的授權與播放 {#licensing-and-playback-for-fairplay}

授權和播放FairPlay保護的內容需要在視訊資訊清單檔案(skd:)中使用的配置與ExpressPlay Token請求(https:)中使用的配置之間，交換URL配置。

從iOS TVSDK用戶端實作授權和播放的指示如下： [在TVSDK應用程式中啟用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)。 您也可以選擇實作FairPlay的離線播放和授權輪換。

## HLS Offline with FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

您可能希望讓使用者在無法擷取授權時，播放受FairPlay保護的內容（例如在飛機上）。

在您開始此工作之前，請先下載並閱讀Apple檔案「 **使用FairPlay串流和HTTP即時串流進行離線播放」**。 閱讀指南以瞭解如何下載傳輸串流(TS)區段並儲存到本機電腦。

透過此工作流程，為FairPlay實作離線播放：

1. 下載HLS TS區段。
1. 向FairPlay伺服器要求永久租用授權(請參 **閱「FairPlay永久租用政策**」)。
1. 儲存 `persistentContentKey`。
1. 離線播放FairPlay內容。

>[!NOTE]
>
>如果持續的內容密鑰已過期，客戶端上的FairPlay流不會開始解密。 不過，如果內容金鑰在播放期間過期，則會繼續使用者體驗。
>
>如需詳 [細資訊，請參閱使用HTTP即時串流](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) (Working with HTTP Live Streaming)檔案。

### FairPlay授權輪換 {#section_D32AA08C61474B4F876AC2A5F18CB879}

授權輪換是防止長期播放內容之授權駭客的方案。

在M3U8資訊清單中，每個金鑰標籤都會套用至下列TS區段，直到下一個金鑰標籤或檔案結束為止。

若要新增授權輪替，請執行下列動作：

* 在授權輪換期間插入新的FairPlay金鑰標籤。

   可新增任何數目的關鍵標籤。

   若為線性內容，請務必在M3U8視窗中維護最新的索引鍵標籤。 iOS會要求下一個M3U8，當仍有大約兩個TS區段可供播放時（約20秒）。 如果新的M3U8包含新的金鑰標籤，所有的金鑰要求都會立即生效。 將不再請求先前的現有密鑰。 iOS會等待所有關鍵要求完成，然後再開始播放。

   對於具有授權旋轉的VOD內容，所有關鍵要求都會在播放開始時發生。

   以下是具有按鍵旋轉的範例M3U8:

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
