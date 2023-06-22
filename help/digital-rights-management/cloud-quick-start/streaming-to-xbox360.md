---
title: 在播放器中設定XSTS權杖
description: 在播放器中設定XSTS權杖
copied-description: true
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 串流至Xbox360 （選購） {#streaming-to-xboc360}

Primetime DRM可在Xbox360平台上使用。 不過，僅支援Protected Streaming使用案例，不支援完整的DRM原則權利。 不支援非串流DRM原則許可權，例如「裝置網域群組」。 嘗試播放內容時，Xbox360會忽略不支援的許可權。

Xbox支援的Primetime DRM原則許可權為：
* 數位輸出保護
* 授權離線快取結束日期
* 授權開始日期
* 授權結束日期
* 播放視窗持續時間（秒）

如果內容已封裝到其他Primetime平台，例如iOS、Android或案頭，則不必重新封裝內容以串流到Xbox360。

對於Xbox360，有個警告是每次在M3U8中遇到EXT-X-KEY標籤時，它都必須連線到金鑰伺服器。 與iOS不同，在DRM原則設定(policy.requireKeyServer)中，iOS Primetime視訊播放器會從localhost擷取AES解密金鑰，而Xbox會一直嘗試從遠端金鑰伺服器擷取解密金鑰。 沒有DRM政策許可權可指示Xbox應用程式從localhost擷取AES解密金鑰。 由於此需求，EXT-X-KEY專案必須位於指向Primetime Cloud DRM端點的M3U8中。 此URL的設定方式： &lt;key_url> OfflinePackager.jar組態檔config_hls.xml中。

如果您想要封裝內容一次，並讓內容串流到所有Primetime目標，以及設定iOS裝置不要從遠端keyserver擷取金鑰，您可以使用具有屬性policy.requireKeyServer=false的DRM原則（例如在policy_ios_localkeyserver.pol中）來封裝內容。 iOS裝置會在本機擷取AES金鑰，而Xbox裝置則會忽略此屬性，並連絡Primetime Cloud DRM金鑰伺服器以取得解密金鑰。

>！注意
>
>所有Xbox360請求都必須使用自訂驗證/>權益。這是因為在Xbox360平台上，Xbox Live會使用Xbox Secure Token Server (XSTS) Token來進行驗證。
>Primetime Cloud DRM授權伺服器使用XSTS權杖來驗證Xbox裝置和發出授權請求的使用者的完整性。 不過，驗證XSTS權杖需要客戶的私人Xbox Live廠商金鑰，而Primetime Cloud DRM不會儲存此金鑰。 因此，當Primetime Cloud DRM收到來自Xbox 360使用者端的授權請求時，Primetime Cloud DRM會將XSTS權杖轉送到Primetime客戶的後端>驗證/權益伺服器。 Primetime客戶的伺服器
>然後會剖析及驗證XSTS權杖，以確保其已使用客戶的應用程式發行者金鑰簽署。
>若要從Xbox360使用者端傳遞XSTS權杖，請同步設定權杖以回應MediaPlayer.RequestKeyAttribute >事件 — 詳情請見此處： **在播放器中設定XSTS權杖。** 軟體發行版本隨附一個範例後端驗證/軟體權利檔案伺服器，位於「自訂驗證」和「軟體權利檔案」目錄中。XSTS權杖的驗證將在此處詳細討論： **Xbox Live XSTS權杖驗證。**


## 在播放器中設定XSTS權杖 {#set-the-xsts-token-in-your-player}

在Xbox360中，您會以非同步方式設定Token以回應 `MediaPlayer.RequestKeyAttribute` 事件。

設定XSTS權杖。

軟體隨附的範例應用程式會顯示如何在播放器中設定XSTS權杖。 以下是範例播放器中的相關程式碼片段：

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Xbox Live XSTS權杖驗證 {#xbox-live-xsts-token-validation}

對於XSTS請求， `customerSpecificAuthToken` 欄位將包含Base64編碼的XSTS權杖。 範例 `XSTSValidator` 程式碼會檢查Base64解碼權杖是否存在 `EncryptedAssertion` 元素；不過，您可以使用其他方法來區分這些請求和非Xbox請求。 例如，您可以使用不同的URL。

回應訊息中傳回的原則將覆寫隨Xbox金鑰請求提供的DRM中繼資料中的原始原則。 Xbox使用者端僅支援原則功能的子集，而且這些欄位是唯一會覆寫原始原則的欄位。

支援權杖解密和驗證需要額外的設定步驟。 您必須載入 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] 認證進入JKS格式金鑰儲存區，然後您提供給後端權益伺服器作為系統屬性 `xsts-keystore`. 依預設，合作夥伴 [!DNL .pfx] 具有別名 `xsts`，而權杖驗證憑證具有別名 `xsts-verify-cert`. 您也可以使用系統屬性來覆寫這些內容。 最後，還有系統屬性 `xsts-keystore-password` 沒有預設值，且包含金鑰庫密碼。 由讀取的系統屬性 `XSTSValidator` 程式碼概述如下：

| 系統屬性 | 預設值 | 註解 |
|---|---|---|
| xsts-keystore | xsts.jks | 驗證器使用的JKS格式金鑰存放區。 |
| xsts-keystore-password |  | 金鑰存放區的密碼 |
| xsts-alias | xsts | 用於從金鑰存放區擷取解密金鑰的別名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用於從金鑰存放區擷取驗證憑證的別名 |

## 建立XSTS驗證器的JKS{#create-jks-for-an-xsts-validator}

1. 瞭解位於合作夥伴中的私人憑證別名 [!DNL .pfx] 檔案。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 轉換 [!DNL .pfx] 至 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步驟1中發現的私人憑證別名。)
1. 匯入 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] ，並定義 `-Dxsts-keystore-password=****` 適用於Tomcat。

若 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密碼，請更新 `xsts` 密碼輸入 `jks` 以維持原樣。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
