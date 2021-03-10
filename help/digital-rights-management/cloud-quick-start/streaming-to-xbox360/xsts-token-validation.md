---
title: Xbox Live XSTS Token驗證
description: Xbox Live XSTS Token驗證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Xbox Live XSTS Token驗證{#xbox-live-xsts-token-validation}

對於XSTS請求，`customerSpecificAuthToken`欄位將包含Base64編碼的XSTS Token。 範例`XSTSValidator`程式碼會檢查Base64解碼Token是否存在`EncryptedAssertion`元素；不過，您可以使用其他方法來區分這些請求與非Xbox請求。 例如，您可以使用不同的URL。

回應訊息中傳回的原則將覆寫隨Xbox金鑰要求提供之DRM中繼資料中的原始原則。 Xbox用戶端僅支援部分原則功能，而且只有這些欄位會覆寫原始原則。

需要額外的設定步驟來支援Token解密和驗證。 您必須將[!DNL xsts_partner_cert.pfx]和[!DNL x_secure_token_service.part.xboxlive.com.cer]憑證載入JKS格式密鑰庫，然後您將其作為系統屬性`xsts-keystore`提供給後端權益伺服器。 預設情況下，夥伴[!DNL .pfx]具有別名`xsts` ，令牌驗證證書具有別名`xsts-verify-cert`。 您也可以使用系統屬性覆寫這些屬性。 最後，系統屬性`xsts-keystore-password`沒有預設值，並包含密鑰庫密碼。 `XSTSValidator`代碼讀取的系統屬性總結如下：

| 系統屬性 | 預設值 | 注釋 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 驗證器使用的JKS格式密鑰庫。 |
| `xsts-keystore-password` |  | 密鑰庫的密碼 |
| `xsts-alias` | `xsts` | 用於從密鑰庫檢索解密密鑰的別名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用於從密鑰庫檢索驗證證書的別名 |

