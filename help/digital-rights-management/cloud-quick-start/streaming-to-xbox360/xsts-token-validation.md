---
title: Xbox Live XSTS權杖驗證
description: Xbox Live XSTS權杖驗證
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Xbox Live XSTS權杖驗證{#xbox-live-xsts-token-validation}

對於XSTS請求， `customerSpecificAuthToken` 欄位將包含Base64編碼的XSTS權杖。 範例 `XSTSValidator` 程式碼會檢查Base64解碼權杖是否存在 `EncryptedAssertion` 元素；不過，您可以使用其他方法來區分這些請求和非Xbox請求。 例如，您可以使用不同的URL。

回應訊息中傳回的原則將覆寫隨Xbox金鑰請求提供的DRM中繼資料中的原始原則。 Xbox使用者端僅支援原則功能的子集，而且這些欄位是唯一會覆寫原始原則的欄位。

支援權杖解密和驗證需要額外的設定步驟。 您必須載入 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] 認證進入JKS格式金鑰儲存區，然後您提供給後端權益伺服器作為系統屬性 `xsts-keystore`. 依預設，合作夥伴 [!DNL .pfx] 具有別名 `xsts`，而權杖驗證憑證具有別名 `xsts-verify-cert`. 您也可以使用系統屬性來覆寫這些內容。 最後，還有系統屬性 `xsts-keystore-password` 沒有預設值，且包含金鑰庫密碼。 由讀取的系統屬性 `XSTSValidator` 程式碼概述如下：

| 系統屬性 | 預設值 | 註解 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 驗證器使用的JKS格式金鑰存放區。 |
| `xsts-keystore-password` |  | 金鑰存放區的密碼 |
| `xsts-alias` | `xsts` | 用於從金鑰存放區擷取解密金鑰的別名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用於從金鑰存放區擷取驗證憑證的別名 |

