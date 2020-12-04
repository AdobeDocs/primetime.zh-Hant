---
description: 'null'
seo-description: 'null'
seo-title: 在您的播放器中設定XSTS Token
title: 在您的播放器中設定XSTS Token
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# 串流至Xbox360（可選）{#streaming-to-xboc360}

Primetime DRM可在Xbox360平台上使用。 不過，僅支援「受保護串流」使用案例，不支援完整的DRM原則權限套件。 不支援非串流DRM原則權限，例如裝置網域群組。 嘗試播放內容時，Xbox360會忽略不支援的權限。

Xbox支援的Primetime DRM政策權利包括：
* 數位輸出保護
* 授權離線快取結束日期
* 授權開始日期
* 授權結束日期
* 播放視窗持續時間（秒）

如果內容已封裝至其他Primetime平台（例如iOS、Android或Desktop），則不必重新封裝內容即可串流至Xbox360。

Xbox360的一個警告是，每次在M3U8中遇到EXT-X-KEY標籤時，Xbox必須始終與關鍵伺服器連接。 與iOS不同，在iOS中，DRM策略設定(policy.requireKeyServer)將導致iOS Primetime視頻播放器從localhost檢索AES解密密鑰，Xbox將始終嘗試從遠程密鑰伺服器檢索解密密鑰。 沒有DRM原則權利指示Xbox應用程式擷取AES解密
localhost的鍵。 因此，EXT-X-KEY項目必須位於指向Primetime Cloud DRM端點的M3U8中。 此URL是透過OfflinePackager.jar組態檔config_hls.xml中的&lt;key_url>設定。

如果您想要封裝內容一次，並讓內容串流至所有Primetime目標，並設定iOS裝置不會從遠端keyserver擷取金鑰，則可使用屬性policy.requireKeyServer=false的DRM原則封裝內容（例如，在policy_ios_localkeyserver.pol中）。 iOS裝置會在本機擷取AES金鑰，而Xbox裝置則會忽略此屬性並觸及Primetime Cloud DRM金鑰伺服器
解密密鑰。

>！注意
>
>所有Xbox360要求都必須使用自訂驗證/>權益。這是因為在Xbox360平台上，Xbox Live >使用Xbox安全代號伺服器(XSTS)代號來進行驗證。
>Primetime Cloud DRM授權伺服器使用XSTS Token來驗證Xbox裝置和發出授權要求的使用者的完整性。 不過，驗證XSTS Token需要>客戶的私人Xbox Live廠商金鑰，Primetime Cloud DRM >不會儲存該金鑰。 因此，當Primetime Cloud DRM收到Xbox 360用戶端的>授權要求時，Primetime Cloud DRM >會將XSTS Token轉送至Primetime客戶的「後端>驗證／權益」伺服器。 Primetime客戶的伺服器
>將會解析並驗證XSTS Token，以確保它是使用客戶的應用程式發行者金鑰>簽署的。
>若要從Xbox360用戶端傳遞XSTS Token，請針對MediaPlayer.RequestKeyAttribute >event同步設定Token —— 詳細說明請參閱：**在您的播放器中設定XSTS Token。** 「自訂驗證」>「權益」目錄中的軟體版本隨附範例後端驗證／權益伺服器>。本軟體將討論XSTS Token的驗證>詳細說明如下： **Xbox Live XSTS代號驗證。**


## 在您的播放器中設定XSTS Token {#set-the-xsts-token-in-your-player}

在Xbox360中，您會以非同步方式設定Token，以回應`MediaPlayer.RequestKeyAttribute`事件。

設定XSTS Token。

軟體隨附的範例應用程式說明如何在您的播放器中設定XSTS Token。 以下是範例播放器中的相關程式碼片段：

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

## Xbox Live XSTS Token驗證{#xbox-live-xsts-token-validation}

對於XSTS請求，`customerSpecificAuthToken`欄位將包含Base64編碼的XSTS Token。 範例`XSTSValidator`程式碼會檢查Base64解碼Token是否存在`EncryptedAssertion`元素；不過，您可以使用其他方法來區分這些請求與非Xbox請求。 例如，您可以使用不同的URL。

回應訊息中傳回的原則將覆寫隨Xbox金鑰要求提供之DRM中繼資料中的原始原則。 Xbox用戶端僅支援部分原則功能，而且只有這些欄位會覆寫原始原則。

需要額外的設定步驟來支援Token解密和驗證。 您必須將[!DNL xsts_partner_cert.pfx]和[!DNL x_secure_token_service.part.xboxlive.com.cer]憑證載入JKS格式密鑰庫，然後您將其作為系統屬性`xsts-keystore`提供給後端權益伺服器。 預設情況下，夥伴[!DNL .pfx]具有別名`xsts` ，令牌驗證證書具有別名`xsts-verify-cert`。 您也可以使用系統屬性覆寫這些屬性。 最後，系統屬性`xsts-keystore-password`沒有預設值，並包含密鑰庫密碼。 `XSTSValidator`代碼讀取的系統屬性總結如下：

| 系統屬性 | 預設值 | 注釋 |
|---|---|---|
| xsts-keystore | xsts.jks | 驗證器使用的JKS格式密鑰庫。 |
| xsts-keystore-password |  | 密鑰庫的密碼 |
| xsts-alias | xsts | 用於從密鑰庫檢索解密密鑰的別名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用於從密鑰庫檢索驗證證書的別名 |

## 為XSTS驗證器建立JKS{#create-jks-for-an-xsts-validator}

1. 查找位於夥伴[!DNL .pfx]檔案中的私有證書的別名。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 將[!DNL .pfx]轉換為[!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   （其中`<alias>`是您在步驟1中發現的私有證書別名）。
1. 導入[!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 將[!DNL xsts.jks]放在Tomcat主目錄中，並定義Tomcat的`-Dxsts-keystore-password=****`。

如果[!DNL xsts_partner_cert.pfx]和[!DNL xsts.jks]使用不同的密碼，請更新`jks`中的`xsts`密碼，使其相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
