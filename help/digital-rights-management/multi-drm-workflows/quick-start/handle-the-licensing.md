---
description: 授權是允許或拒絕用戶播放受保護視頻內容的主要機制。 合法（有權）用戶可以被頒發許可證（密鑰）以解密和播放其內容提供商的加密內容的特定部分。
title: 許可
exl-id: 60aa3e77-f821-41b3-ba0e-1a2c05b2bb1a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 許可{#licensing}

授權是允許或拒絕用戶播放受保護視頻內容的主要機制。 合法（有權）用戶可以被頒發許可證（密鑰）以解密和播放其內容提供商的加密內容的特定部分。

在最終用戶設備上的應用或網頁可以播放受DRM保護的內容之前，它必須從您（客戶）操作的權利或店面伺服器獲取令牌。 Adobe為此目的提供了示例參考伺服器： [參考伺服器：示例ExpressPlay權利伺服器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)。

您的權利檔案或店面伺服器將從相關的ExpressPlay伺服器請求許可證令牌，只有在與您自己的後端系統進行檢查以確定特定用戶是否有權查看請求的內容之後，才會這樣做。 從許可證令牌請求返回的響應是許可證伺服器的可隨時使用的URL，或響應包含JSON結構中的URL，具體取決於您正在使用的DRM解決方案。

>[!NOTE]
>
>無法從客戶端本身發出許可證令牌請求：
>1. 必須在受信任的環境中檢查權利；和
>1. 必須保密客戶驗證器。


1. 發出許可證令牌請求。

   對於快速啟動方案，您只需要確保所涉及的各個元件協同工作，您可能需要使用類似 [!DNL curl] 發出許可證令牌請求（而不是最初讓應用程式啟動並運行並測試來自該應用程式的呼叫）。 例如：

   * 維德文：

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

   Widevinetest標籤示例：

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   請注意，Widevine響應是「隨時可用」URL字串。

   * PlayReady:

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

   示例PlayReadytest令牌：

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   請注意，PlayReady響應是JSON對象，具有單獨的URL和令牌元素。

   * 公平遊戲：

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

   示例FairPlaytest令牌：

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   請注意，FairPlay響應是「隨時可用」URL字串。
