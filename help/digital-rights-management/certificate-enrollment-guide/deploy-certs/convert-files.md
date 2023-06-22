---
title: 轉換檔案
description: 轉換檔案
copied-description: true
exl-id: 7344ca2f-5307-403b-a6fc-cbbea7c2829f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 轉換檔案{#convert-files}

請求者使用公用程式（例如OpenSSL和私密金鑰）從命令視窗輸入下列命令來產生PKCS#12 (pfx)和PEM/DER檔案：

1. 將PKCS#7檔案轉換為暫存PEM檔案。

   若要使用OpenSSL，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >此暫時PEM包含您的憑證和中繼CA的憑證。 使用這些憑證來產生PFX檔案。

1. 將暫存PEM檔案轉換為PFX檔案。

   若要使用OpenSSL，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. 將暫存PEM檔案轉換為最終PEM檔案。

   若要使用OpenSSL，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >雖然不需要，但Adobe建議對私密金鑰(private_key_password)和PFX (pfx_password)使用不同的密碼。

   此最終PEM檔案僅包含您的憑證。

1. 將PEM檔案轉換為DER檔案。

   若要使用OpenSSL，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >只有HTTP Dynamic Streaming封裝程式才需要DER檔案。
