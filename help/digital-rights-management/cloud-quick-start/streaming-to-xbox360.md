---
title: 在播放器中設定XSTS令牌
description: 在播放器中設定XSTS令牌
copied-description: true
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 流式處理到Xbox360（可選） {#streaming-to-xboc360}

黃金時段DRM可在Xbox360平台上使用。 但是，只支援「受保護的流」使用案例，而不支援全套DRM策略權限。 不支援非流式DRM策略權限，如設備域組。 Xbox360在嘗試播放內容時會忽略不受支援的權限。

Xbox的Bogk時段DRM政策支援權限包括：
* 數字輸出保護
* 許可證離線快取結束日期
* 許可證開始日期
* 許可證結束日期
* 播放窗口持續時間（秒）

如果內容已打包用於其他黃金時段平台，如iOS、Android或案頭，則可能不必重新打包以流式傳輸到Xbox360。

Xbox360的一個注意事項是，每次在M3U8中遇到EXT-X-KEY標籤時，它必須始終聯繫到密鑰伺服器。 與iOS不同，在iOS,DRM策略設定(policy.requireKeyServer)將導致黃金時段視頻播放器從本地主機檢索AES解密密鑰，Xbox將始終嘗試從遠程密鑰伺服器檢索解密密鑰。 沒有DRM策略權限指示Xbox應用從本地主機檢索AES解密密鑰。 由於這一要求，EXT-X-KEY條目必須位於指向黃金時段雲DRM端點的M3U8中。 此URL是通過 &lt;key_url> 在OfflinePackager.jar配置檔案config_hls.xml中。

如果希望將內容打包一次並使其流到所有黃金時段目標，並將iOS設備配置為不從遠程密鑰伺服器檢索密鑰，則可以使用屬性policy.requireKeyServer=false的DRM策略來打包內容（如policy_ios_localkeyserver.pol中）。 iOS設備將在本地檢索AES密鑰，而Xbox設備將忽略此屬性並訪問黃金時段雲DRM密鑰伺服器獲取解密密鑰。

>！注釋
>
>所有Xbox360請求都必須使用自定義身份驗證/>權利。這是因為在Xbox360平台上，Xbox Live >使用Xbox安全令牌伺服器(XSTS)令牌用於>驗證目的。
>黃金時段雲DRM許可證伺服器使用XSTS令牌>驗證Xbox設備和用戶發出的許可證請求的完整性。 但是，驗證XSTS令牌需要>客戶的專用Xbox Live供應商密鑰，而Mighide Cloud DRM>不儲存該密鑰。 因此，當黃金時段雲DRM收到Xbox 360客戶端的>一個許可請求時，黃金時段雲DRM >將將XSTS令牌轉發到黃金時段客戶的後端>驗證/權利伺服器。 黃金時段客戶伺服器
>然後將分析並驗證XSTS令牌，以確保它已使用客戶的應用程式發佈者密鑰簽名。
>要從Xbox360客戶端傳遞XSTS令牌，請響應MediaPlayer.RequestKeyAttribute >event（此處進一步詳述），請同步設定令牌>: **在播放器中設定XSTS令牌。** 在「自定義驗證」>和「權利」目錄中，軟體版本中包含一個「後端驗證/權利」伺服器示例。XSTS令牌的驗證將在以下位置進行詳細討論： **Xbox Live XSTS令牌驗證。**


## 在播放器中設定XSTS令牌 {#set-the-xsts-token-in-your-player}

在Xbox360中，您非同步設定令牌以響應 `MediaPlayer.RequestKeyAttribute` 的子菜單。

設定XSTS令牌。

與軟體捆綁的示例應用說明如何在播放器中設定XSTS令牌。 下面是示例播放器中的相關代碼段：

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

## Xbox Live XSTS令牌驗證 {#xbox-live-xsts-token-validation}

對於XSTS請求， `customerSpecificAuthToken` 欄位將包含Base64編碼的XSTS令牌。 示例 `XSTSValidator` 代碼檢查Base64解碼的令牌是否存在 `EncryptedAssertion` 元素；但是，您可以使用其他方法來區分這些請求和非Xbox請求。 例如，可以使用其他URL。

在響應消息中返回的策略將覆蓋隨Xbox密鑰請求提供的DRM元資料中的原始策略。 Xbox客戶端只支援策略功能的子集，這些欄位是唯一將覆蓋原始策略的欄位。

需要其他設定步驟來支援令牌解密和驗證。 必須載入 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] JKS格式密鑰庫中的憑據，然後將其作為系統屬性提供給後端權利伺服器 `xsts-keystore`。 預設情況下，合作夥伴 [!DNL .pfx] 有別名 `xsts`，令牌驗證證書具有別名 `xsts-verify-cert`。 也可以使用系統屬性覆蓋這些屬性。 最後，有一個系統屬性 `xsts-keystore-password` 沒有預設值，並且包含密鑰庫密碼。 由 `XSTSValidator` 規則概述如下：

| 系統屬性 | 預設值 | 注釋 |
|---|---|---|
| xsts密鑰庫 | xsts.jks | 驗證程式使用的JKS格式密鑰庫。 |
| xsts-keystore-password |  | 密鑰庫的密碼 |
| xsts別名 | xst | 用於從密鑰庫檢索解密密鑰的別名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用於從密鑰庫檢索驗證證書的別名 |

## 為XSTS驗證程式建立JKS{#create-jks-for-an-xsts-validator}

1. 查找位於合作夥伴中的專用證書的別名 [!DNL .pfx] 的子菜單。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 轉換 [!DNL .pfx] 至 [!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   ( `<alias>` 是您在步驟1中發現的專用證書的別名。)
1. 導入 [!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 放置 [!DNL xsts.jks] 在Tomcat主目錄中，並定義 `-Dxsts-keystore-password=****` 的雙曲餘切值。

如果 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密碼，更新 `xsts` 密碼 `jks` 讓他們變成一樣。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
