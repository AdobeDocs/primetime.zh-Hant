---
description: 授權是允許或拒絕使用者播放受保護視訊內容的主要機制。 合法（已授權）的使用者可獲得授權（金鑰），以解密並播放其內容供應商的加密內容。
seo-description: 授權是允許或拒絕使用者播放受保護視訊內容的主要機制。 合法（已授權）的使用者可獲得授權（金鑰），以解密並播放其內容供應商的加密內容。
seo-title: 授權
title: 授權
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# 授權{#licensing}

授權是允許或拒絕使用者播放受保護視訊內容的主要機制。 合法（已授權）的使用者可獲得授權（金鑰），以解密並播放其內容供應商的加密內容。

在使用者裝置上的應用程式或網頁播放受DRM保護的內容之前，它必須從您（客戶）操作的權益或店面伺服器取得Token。 Adobe提供範例參考伺服器，以供下列用途使用： [參考伺服器：範例ExpressPlay Entitlement Server(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)。

您的權益或店面伺服器必須先向相關的ExpressPlay伺服器要求授權Token，然後再與您自己的後端系統進行檢查，以判斷特定使用者是否有權觀看要求的內容。 從授權Token請求傳回的回應是授權伺服器的現成可用URL，或回應包含JSON結構中的URL，視您使用的DRM解決方案而定。

>[!NOTE]
>
>無法從用戶端本身提出授權Token要求：
>1. 這些權利必須在受信任的環境中進行檢查；和
>1. 客戶驗證器必須保密。


1. 提出授權Token要求。

   若是快速啟動的案例（您只想確定相關的各種元件彼此搭配運作），您可能會想使用類似的方式來提出授權Token要求（而不是一開始啟動應用程式並從那裡執行和測試呼叫）。 [!DNL curl] 例如：

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   範例Widevine測試Token:

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   請注意，Widevine回應是「現成可用」的URL字串。

   * 播放就緒：

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   範例PlayReady測試Token:

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   請注意，PlayReady回應是JSON物件，具有個別的URL和Token元素。

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   範例FairPlay測試Token:

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   請注意，FairPlay回應是「現成可用」的URL字串。
