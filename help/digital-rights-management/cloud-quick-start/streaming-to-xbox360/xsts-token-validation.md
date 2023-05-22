---
title: Xbox Live XSTS令牌驗證
description: Xbox Live XSTS令牌驗證
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Xbox Live XSTS令牌驗證{#xbox-live-xsts-token-validation}

對於XSTS請求， `customerSpecificAuthToken` 欄位將包含Base64編碼的XSTS令牌。 示例 `XSTSValidator` 代碼檢查Base64解碼的令牌是否存在 `EncryptedAssertion` 元素；但是，您可以使用其他方法來區分這些請求和非Xbox請求。 例如，可以使用其他URL。

在響應消息中返回的策略將覆蓋隨Xbox密鑰請求提供的DRM元資料中的原始策略。 Xbox客戶端只支援策略功能的子集，這些欄位是唯一將覆蓋原始策略的欄位。

需要其他設定步驟來支援令牌解密和驗證。 必須載入 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] JKS格式密鑰庫中的憑據，然後將其作為系統屬性提供給後端權利伺服器 `xsts-keystore`。 預設情況下，合作夥伴 [!DNL .pfx] 有別名 `xsts`，令牌驗證證書具有別名 `xsts-verify-cert`。 也可以使用系統屬性覆蓋這些屬性。 最後，有一個系統屬性 `xsts-keystore-password` 沒有預設值，並且包含密鑰庫密碼。 由 `XSTSValidator` 規則概述如下：

| 系統屬性 | 預設值 | 注釋 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 驗證程式使用的JKS格式密鑰庫。 |
| `xsts-keystore-password` |  | 密鑰庫的密碼 |
| `xsts-alias` | `xsts` | 用於從密鑰庫檢索解密密鑰的別名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用於從密鑰庫檢索驗證證書的別名 |

