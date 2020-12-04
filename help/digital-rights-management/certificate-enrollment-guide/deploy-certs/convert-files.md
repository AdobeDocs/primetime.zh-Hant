---
seo-title: 轉換檔案
title: 轉換檔案
uuid: e17ee003-5ac2-4bb8-83b7-81ee8fa9ee46
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 轉換檔案{#convert-files}

請求者使用OpenSSL和私鑰等實用程式，通過從命令窗口輸入以下命令來生成PKCS#12(pfx)和PEM/DER檔案：

1. 將PKCS#7檔案轉換為暫存PEM檔案。

   要使用OpenSSL，請開啟命令窗口並輸入以下內容：

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >此臨時PEM包含您的證書和中級CA的證書。 使用這些憑證來產生PFX檔案。

1. 將臨時PEM檔案轉換為PFX檔案。

   要使用OpenSSL，請開啟命令窗口並輸入以下內容：

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. 將臨時PEM檔案轉換為最終PEM檔案。

   要使用OpenSSL，請開啟命令窗口並輸入以下內容：

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >雖然不需要，Adobe建議針對私密金鑰(private_key_password)和PFX(pfx_password)使用不同的密碼。

   此最終PEM檔案僅包含您的證書。

1. 將PEM檔案轉換為DER檔案。

   要使用OpenSSL，請開啟命令窗口並輸入以下內容：

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER檔案僅適用於HTTP動態串流封裝。

