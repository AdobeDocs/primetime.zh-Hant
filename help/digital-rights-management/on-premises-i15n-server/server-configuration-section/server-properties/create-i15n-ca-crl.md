---
title: 建立個性化CA CRL
description: 建立個性化CA CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 建立個性化CA CRL{#create-individualization-ca-crl}

該證書撤銷清單(CRL)分發點包含在由個性化伺服器頒發的每台電腦證書中。 在授權伺服器上的機器憑證驗證期間，此CRL將從憑證中所列的散布點下載(或從快取中讀取（如果已下載），並檢查以確保憑證未被撤銷。

>[!NOTE]
>
>要設定CRL分發點的URL，您需要設定[!DNL AdobeInitial.properties] `cert.machine.crldp`欄位。 此散布點由Primetime DRM檢查是否有效。 **&#x200B;您必須確認此URL有效。 除非從授權伺服器出現驗證錯誤，否則無效URL所產生的錯誤不會明顯。

以下簡單說明使用OpenSSL建立授權伺服器可使用之CRL的範例說明。 Adobe建議您在取得Production Indificialization CA憑證後，以安全的方式和環境執行這些步驟。

1. 將工作目錄更改為此分發中包含的[!DNL create_crl]目錄。
1. 將個人化CA [!DNL pfx]複製到相同的[!DNL create_crl]目錄。

   後續步驟假定個性化CA pfx命名為[!DNL i15n.pfx]。 視需要調整設定。
1. 解壓個性化CA [!DNL pfx]檔案的私鑰。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 將私密金鑰轉換為[!DNL pksc8]格式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例建立具有預設1個月有效期的CRL。 使用`-crldays`和`-crlhours`選項來覆蓋預設值。

   生成CRL時，使用[!DNL openssl.conf]中指向的[!DNL index]和[!DNL crlnumber]檔案。 預設情況下，使用工作目錄中的[!DNL demoCA]位置。 提供的[!DNL demoCA]目錄中包含示例[!DNL index]和[!DNL crlnumber]檔案。

1. 將在上一步中生成的CRL檔案部署到許可伺服器可以訪問的適當位置(例如：個人化伺服器[!DNL ROOT])。
1. CRL就位後，重新啟動授權伺服器。
