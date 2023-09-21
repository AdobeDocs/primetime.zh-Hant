---
description: 授權是允許或拒絕使用者播放受保護視訊內容的主要機制。 合法的（有權利的）使用者可獲發授權（金鑰），以解密及播放其內容提供者的特定加密內容。
title: 授權
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 授權{#licensing}

授權是允許或拒絕使用者播放受保護視訊內容的主要機制。 合法的（有權利的）使用者可獲發授權（金鑰），以解密及播放其內容提供者的特定加密內容。

在使用者裝置上的應用程式或網頁可以播放受DRM保護的內容之前，必須從您客戶所操作的權利或店面伺服器取得Token。 Adobe為此提供範例參考伺服器： [參考伺服器：範例ExpressPlay軟體權利檔案伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

您的軟體權利檔案或店面伺服器會向相關的ExpressPlay伺服器要求授權權杖，但前提是與您自己的後端系統核實，以確定特定使用者是否有權觀看要求的內容。 從授權權杖請求傳回的回應可能是授權伺服器的現成可用URL，或回應包含JSON結構的URL，具體取決於您使用的DRM解決方案。

>[!NOTE]
>
>無法從使用者端本身提出授權權杖請求：
>1. 必須在受信任的環境中檢查權利；以及
>1. 客戶驗證器必須保密。

1. 提出授權Token要求。

   對於快速入門案例，您只想確保所涉及的各種元件能夠共同運作，您可能會想要使用類似以下的專案 [!DNL curl] 發出授權Token要求（而非讓應用程式初次啟動，並從那裡執行及測試呼叫）。 例如：

   * Widevine：

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

   Widevine測試權杖範例：

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   請注意，Widevine回應是「準備使用」的URL字串。

   * PlayReady：

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

   PlayReady測試權杖範例：

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   請注意，PlayReady回應是JSON物件，具有個別的URL和權杖元素。

   * FairPlay：

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

   範例FairPlay測試權杖：

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   請注意，FairPlay回應是「準備使用」的URL字串。
