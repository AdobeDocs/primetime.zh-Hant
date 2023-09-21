---
title: 建立個人化CA CRL
description: 建立個人化CA CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 建立個人化CA CRL{#create-individualization-ca-crl}

此憑證撤銷清單(CRL)散發點包含在個人化伺服器所發行的每個電腦憑證中。 在授權伺服器上進行電腦憑證驗證期間，將從憑證所列的分發點下載此CRL （如果已經下載，則從快取讀取），並檢查以確定憑證尚未被撤銷。

>[!NOTE]
>
>若要設定CRL發佈點的URL，您必須設定 [!DNL AdobeInitial.properties] `cert.machine.crldp` 欄位。 此發佈點為 *非* 已由Primetime DRM檢查有效性。 您必須確認此URL有效。 除非授權伺服器出現驗證錯誤，否則無效URL所造成的錯誤不會顯現。

以下為使用OpenSSL建立您的授權伺服器可以使用的CRL的簡化範例指示。 Adobe建議您在取得生產個人化CA認證後，以安全的方式和環境執行這些步驟。

1. 將工作目錄變更為 [!DNL create_crl] 包含在此散發中的目錄。
1. 複製您的個人化CA [!DNL pfx] 至相同 [!DNL create_crl] 目錄。

   後續步驟假設已命名個人化CA pfx [!DNL i15n.pfx]. 視需要調整您的設定。
1. 擷取個人化CA [!DNL pfx] 檔案的私密金鑰。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 將私密金鑰轉換為 [!DNL pksc8] 格式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 產生CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此範例會建立具有預設1個月有效期間的CRL。 使用 `-crldays` 和 `-crlhours` 覆蓋預設值的選項。

   產生CRL時會使用 [!DNL index] 和 [!DNL crlnumber] 檔案指向您的 [!DNL openssl.conf]. 根據預設， [!DNL demoCA] 使用工作目錄中的位置。 範例 [!DNL index] 和 [!DNL crlnumber] 檔案包含在提供的 [!DNL demoCA] 目錄。

1. 將上一步驟中產生的CRL檔案部署至授權伺服器可存取的適當位置（例如：個人化伺服器） [!DNL ROOT])。
1. 在CRL就位後，重新啟動授權伺服器。
