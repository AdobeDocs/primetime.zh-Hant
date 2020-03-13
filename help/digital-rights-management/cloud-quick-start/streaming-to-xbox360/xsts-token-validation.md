---
seo-title: Xbox Live XSTS Token驗證
title: Xbox Live XSTS Token驗證
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Xbox Live XSTS Token驗證{#xbox-live-xsts-token-validation}

對於XSTS請求，欄 `customerSpecificAuthToken` 位將包含Base64編碼的XSTS Token。 范常式 `XSTSValidator` 式碼會檢查Base64解碼Token是否存在元 `EncryptedAssertion` 素；不過，您可以使用其他方法來區分這些請求與非Xbox請求。 例如，您可以使用不同的URL。

回應訊息中傳回的原則將覆寫隨Xbox金鑰要求提供之DRM中繼資料中的原始原則。 Xbox用戶端僅支援部分原則功能，而且只有這些欄位會覆寫原始原則。

需要額外的設定步驟來支援Token解密和驗證。 您必須將 [!DNL xsts_partner_cert.pfx] 和憑證載入 [!DNL x_secure_token_service.part.xboxlive.com.cer] JKS格式密鑰庫中，然後您將其作為系統屬性提供給後端權益伺服器 `xsts-keystore`。 預設情況下，合作伙 [!DNL .pfx] 伴具有別名 `xsts`，令牌驗證證書具有別名 `xsts-verify-cert`。 您也可以使用系統屬性覆寫這些屬性。 最後，有一個系統屬 `xsts-keystore-password` 性沒有預設值，並包含密鑰庫密碼。 代碼讀取的系統 `XSTSValidator` 屬性概述如下：

| 系統屬性 | 預設值 | 注釋 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 驗證器使用的JKS格式密鑰庫。 |
| `xsts-keystore-password` |  | 密鑰庫的密碼 |
| `xsts-alias` | `xsts` | 用於從密鑰庫檢索解密密鑰的別名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用於從密鑰庫檢索驗證證書的別名 |

