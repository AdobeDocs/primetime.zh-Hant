---
title: 建立個性化CA CRL
description: 建立個性化CA CRL
copied-description: true
exl-id: 72147209-1337-4aed-9e4e-210c905c55a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 建立個性化CA CRL{#create-individualization-ca-crl}

此證書吊銷清單(CRL)分發點包含在由個性化伺服器頒發的每個電腦證書中。 在許可證伺服器上的電腦證書驗證期間，將從證書中列出的分發點下載此CRL（如果已下載，則從快取中讀取），並檢查以確保證書未被吊銷。

>[!NOTE]
>
>要設定CRL分發點的URL，需要設定 [!DNL AdobeInitial.properties] `cert.machine.crldp` 的子菜單。 此分發點 *不* 已由黃金時段DRM檢查有效性。 必須驗證此URL是否有效。 在許可證伺服器中出現驗證錯誤之前，無效URL導致的錯誤不會變得明顯。

下面概述的示例說明是使用OpenSSL建立許可證伺服器可以使用的CRL。 Adobe建議您在獲得「生產個性化CA」憑據後，以安全的方式和環境執行這些步驟。

1. 將工作目錄更改為 [!DNL create_crl] 目錄。
1. 複製您的個性化CA [!DNL pfx] 到相同 [!DNL create_crl] 的子菜單。

   後續步驟假定個性化CA pfx命名 [!DNL i15n.pfx]。 根據設定進行適當調整。
1. 提取個性化CA [!DNL pfx] 檔案的私鑰。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 將私鑰轉換為 [!DNL pksc8] 的子菜單。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例建立一個CRL，預設有效期為1個月。 使用 `-crldays` 和 `-crlhours` 選項以覆蓋預設值。

   生成CRL時使用 [!DNL index] 和 [!DNL crlnumber] 指向 [!DNL openssl.conf]。 預設情況下， [!DNL demoCA] 使用工作目錄中的位置。 示例 [!DNL index] 和 [!DNL crlnumber] 檔案包含在提供的檔案中 [!DNL demoCA] 的子菜單。

1. 將上一步中生成的CRL檔案部署到許可證伺服器可訪問的適當位置(例如：個性化伺服器 [!DNL ROOT])。
1. CRL到位後，重新啟動許可證伺服器。
