---
seo-title: 建立個性化CA CRL
title: 建立個性化CA CRL
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 建立個性化CA CRL{#create-individualization-ca-crl}

該證書撤銷清單(CRL)分發點包含在由個性化伺服器頒發的每台電腦證書中。 在授權伺服器上的機器憑證驗證期間，此CRL將從憑證中所列的散布點下載(或從快取中讀取（如果已下載），並檢查以確保憑證未被撤銷。

>[!NOTE]
>
>要設定CRL分發點的URL，您需要設定字 [!DNL AdobeInitial.properties]`cert.machine.crldp` 段。 Primetime DRM不會檢 *查此* 散布點是否有效。 您必須確認此URL有效。 除非從授權伺服器出現驗證錯誤，否則無效URL所產生的錯誤不會明顯。

以下簡單說明使用OpenSSL建立授權伺服器可使用之CRL的範例說明。 Adobe建議您在取得Production Indificialization CA憑證後，以安全的方式和環境執行這些步驟。

1. 將工作目錄更改為此分 [!DNL create_crl] 發包含的目錄。
1. 將您的個人化CA [!DNL pfx] 複製至相同 [!DNL create_crl] 目錄。

   後續步驟假設個人化CA pfx是命名的 [!DNL i15n.pfx]。 視需要調整設定。
1. 摘取個人化CA [!DNL pfx] 檔案的私密金鑰。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 將私密金鑰轉換為 [!DNL pksc8] 格式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例建立具有預設1個月有效期的CRL。 使用和 `-crldays` 選 `-crlhours` 項來覆寫預設值。

   生成CRL時，會使 [!DNL index] 用您 [!DNL crlnumber] 中指向的和檔案 [!DNL openssl.conf]。 預設情況下， [!DNL demoCA] 使用工作目錄中的位置。 示例 [!DNL index] 和 [!DNL crlnumber] 檔案包含在提供的目 [!DNL demoCA] 錄中。

1. 將在上一步中生成的CRL檔案部署到許可伺服器可以訪問的適當位置(例如：個人化伺服 [!DNL ROOT]器)。
1. CRL就位後，重新啟動授權伺服器。
