---
description: DRM工作流程包括封裝您的內容、提供內容的授權，以及從您自己的視訊應用程式播放受保護的內容。 每個DRM解決方案的工作流程通常都類似，但細節上有些差異。
title: 公平播放的多重DRM工作流程
exl-id: a66cecda-762b-48f7-afed-6fef6303d169
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 公平播放的多重DRM工作流程 {#multi-drm-workflow-for-fairplay}

DRM工作流程包括封裝您的內容、提供內容的授權，以及從您自己的視訊應用程式播放受保護的內容。 每個DRM解決方案的工作流程通常都類似，但細節上有些差異。

此多DRM工作流程會帶您完成Apple FairPlay所保護之HLS內容的設定、封裝、授權和播放。 此工作流程也包含實作離線播放和授權輪換的選用指示。

## 啟用FairPlay的ExpressPlay服務 {#enable-expressplay-service-for-fairplay}

當您搭配ExpressPlay DRM服務使用Apple的FairPlay DRM解決方案時，需要一些設定。 其中涉及從Apple取得認證，並將其上傳至ExpressPlay。

請依照下列步驟啟用ExpressPlay服務，以提供FairPlay內容保護。

1. 從Apple取得認證。

   這些認證會唯一提供給每個服務提供者。 您必須完成下清單單來要求這些許可權： [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >選取 **[!UICONTROL Content Provider]** 用於主要角色。

   您的請求獲得核准後，Apple會傳送電子郵件給您。 *FairPlay串流部署套件*.
1. 產生憑證申請檔。

   您可以使用 [!DNL openssl] 以產生您的公開/私密金鑰組，以及您的憑證簽署要求(CSR)。

   1. 產生您的金鑰組。

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
      >此步驟的指示位於 *FairPlay串流部署套件*，但為了您的方便，也包含在這裡。 如果您對流程的這個部分有任何問題，請檢視 *FairPlayCertificateCreation.pdf* （在您的部署套件中）。

1. 透過Apple開發人員入口網站上傳您的CSR。
   1. 開發團隊的團隊代理必須登入 [!DNL developer.apple.com/account].
   1. 按一下 **[!UICONTROL Certificates, Identifiers & Profiles]**，然後選取 **[!UICONTROL iOS, tvOS, watchOS]** 下拉式清單，然後按一下 **[!UICONTROL Certificates->Production]** 頁面左側。
   1. 按一下 **[!UICONTROL +]** 按鈕來要求新憑證。 選取 **[!UICONTROL FairPlay Streaming Certificate]** 下的選項 **[!UICONTROL Production]**.

      此 *新增iOS憑證* 對話方塊開啟。
   1. 在 *新增iOS憑證*，上傳您在步驟2.b.中產生的CSR檔案，然後按一下 **[!UICONTROL Generate]**.

      您的應用程式秘密金鑰(ASK)會顯示在同一個對話方塊中。
   1. 記下您的ASK，並將其儲存在安全的位置。
   1. 在ASK中取得金鑰以完成憑證產生並按一下 **[!UICONTROL Continue]**.
   1. 確認已儲存ASK之後，請按一下 **[!UICONTROL Generate]** 以繼續。

      >[!NOTE]
      >
      >請務必儲存ASK的復本並妥善儲存。 *如果您的ASK受到損害，您將無法再使用FairPlay串流保護您的內容。* 只有一(1)個ASK分配給您的團隊。 不會再提供值，且您稍後無法擷取它。

   1. 下載您的FPS憑證。

      請務必將私密金鑰（來自步驟2.a.）和公開金鑰（您在此步驟中下載的FPS憑證）的備份復本儲存在安全的地方。
1. 使用您的FairPlay憑證設定您的ExpressPlay帳戶。
   1. 假設您在步驟3.h.下載的憑證名稱是 [!DNL fairplay.cer].
   1. 開啟 [!DNL fairplay.cer] 使用Apple鑰匙圈存取公用程式的檔案。
   1. 輸入「」以篩選許多憑證 `fairplay`」在右上角的搜尋欄位中。
   1. 識別貴公司的FairPlay憑證。

      您的公司名稱應與Apple發行的憑證相關聯。
   1. 選取展開箭頭來展開憑證，然後以滑鼠右鍵按一下您的私密金鑰。
   1. 選取 **[!UICONTROL Export "Your Company Name"]** 並儲存 [!DNL .p12] 檔案。

      系統會要求您指定密碼來保護此檔案。 記下此密碼，因為您將需要連同認證封裝一起傳送此密碼。
   1. 於登入您的帳戶 [www.expressplay.com](https://www.expressplay.com).
   1. 按一下 **[!UICONTROL DRM SERVICES]** 然後選取「 」 **[!UICONTROL FairPlay]** 標籤。
   1. 將您的FairPlay憑證上傳至您的ExpressPlay帳戶。

      1. 建立包含ASK值的文字檔(應該是32個字元，例如： `1234567890abcdef1234567890abcdef`)，並選取此檔案以上傳。
      1. 從Step 4.f.選取要上傳的PKCS12檔案。
      1. 從Step 4.f輸入PKCS12檔案密碼。
      1. 按一下上傳按鈕。

現在您可以建立iOS應用程式或HTML5頁面，並搭配您的 [!DNL fairplay.cer] 憑證使用FairPlay的ExpressPlay服務。

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### 封裝您的內容以享受FairPlay {#package-your-content-for-fairplay}

若要封裝您的內容，您可以使用AdobeOffline Packager或其他工具，例如ExpressPlay的Bento4封裝。

封裝程式會準備視訊以進行播放（例如，將原始檔案分割並放入資訊清單中），並使用您選擇的DRM解決方案（在此案例中為FairPlay）來保護視訊：

* [FairPlay DRM的Adobe離線封裝程式](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay封裝程式 — 適用於HLS的Bento4](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 封裝您的內容。

   以下是使用Adobe Offline Packager的封裝範例。 封裝程式會使用組態檔(例如 [!DNL fairplay.xml])，如下所示：

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

   * `in_path`  — 此專案指向本機封裝電腦上的來源視訊位置。
   * `out_type`  — 此專案說明封裝輸出的型別，在此例中為FairPlay的HLS。
   * `out_path`  — 本機電腦上您要輸出到的位置。
   * `drm_sys`  — 您封裝的DRM解決方案。 這是 `FAIRPLAY` 在此案例中。
   * `frag_dur`  — 片段持續時間（秒）。
   * `target_dur` - HLS輸出的目標持續時間。
   * `key_file_path`  — 這是封裝電腦上用作內容加密金鑰(CEK)的授權檔案的位置。 它是Base-64編碼的16位元組十六進位字串。
   * `iv_file_path`  — 這是封裝機器上IV檔案的位置。
   * `key_url`  — 的URI引數 `EXT-X-KEY` 的標籤 [!DNL .m3u8] 檔案。
   * `content_id`  — 預設值。

   如 [Packager檔案](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)，「最佳做法是建立組態檔，其中包含您要用來產生輸出的常用選項。 然後，提供特定選項作為命令列引數來建立輸出。」

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   產生的M3U8檔案具有 `EXT-X-KEY` 屬性，如下所示：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### 設定FairPlay的原則 {#setting-policies-for-fairplay}

您可以使用軟體權利檔案伺服器，為受FairPlay保護的內容設定原則。 您可以自行設定，或使用Adobe提供的範例權益伺服器。

Adobe提供範例ExpressPlay軟體權利檔案伺服器(SEES)，說明如何操作 *基於時間* 和 *裝置繫結* 權利。 此範例軟體權利檔案伺服器是以ExpressPlay服務為基礎所建置。

[參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [參考服務：以時間為基礎的權益](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [參考服務：裝置繫結權益](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay的授權和播放 {#licensing-and-playback-for-fairplay}

FairPlay保護內容的授權和播放需要交換URL配置，在視訊資訊清單檔案(skd：)中使用的配置和ExpressPlay權杖請求(https：)中使用的配置之間。

以下說明如何從iOS TVSDK使用者端實作授權和播放： [在TVSDK應用程式中啟用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). 您也可以選擇實作FairPlay的離線播放和授權輪換。

## 使用FairPlay離線HLS {#section_047A05D1E3B64883858BC601CFC8F759}

您可能想要讓使用者在無法擷取其授權時播放受FairPlay保護的內容，因為播放器與網路隔離（例如在飛機上）。

開始此工作之前，請先下載並閱讀Apple檔案 **「使用FairPlay串流和HTTP即時串流進行離線播放」**. 閱讀指南以瞭解如何下載Transport Stream (TS)區段並將它們儲存到您的本機電腦。

使用此工作流程實作FairPlay的離線播放：

1. 下載HLS TS區段。
1. 向FairPlay伺服器要求永久租用授權(請參閱 **「FairPlay持續性租賃政策」**)。
1. 儲存 `persistentContentKey`.
1. 離線播放FairPlay內容。

>[!NOTE]
>
>如果儲存的內容金鑰已過期，使用者端上的FairPlay串流不會開始解密。 不過，如果內容索引鍵在播放期間過期，則會繼續使用者體驗。
>
>另請參閱 [使用HTTP即時資料流](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) 檔案，以取得更多詳細資料。

### FairPlay授權輪換 {#section_D32AA08C61474B4F876AC2A5F18CB879}

授權輪換是一種防止長時間播放的內容遭到授權駭客攻擊的方案。

在M3U8資訊清單中，每個金鑰標籤會套用至下列TS區段，直到下一個金鑰標籤或檔案結尾為止。

若要新增授權輪換，請執行下列動作：

* 在授權輪換期間插入新的FairPlay金鑰標籤。

   可新增任意數量的關鍵標籤。

   如果是線性內容，請務必在M3U8視窗中保留最新的金鑰標籤。 大約還剩兩個TS區段可供播放時（約20秒），iOS會要求下一個M3U8。 如果新的M3U8包含新的關鍵標籤，所有關鍵請求都將立即發生。 將不再請求先前的現有金鑰。 iOS會等待所有重要要求完成，再開始播放。

   對於使用授權輪換的VOD內容，所有重要請求都將在播放開始時發生。

   以下是包含金鑰輪換的範例M3U8：

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
