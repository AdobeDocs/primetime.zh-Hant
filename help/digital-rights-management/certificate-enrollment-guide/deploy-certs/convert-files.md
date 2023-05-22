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

請求者使用諸如OpenSSL和私鑰之類的實用程式通過在命令窗口中輸入以下命令來生成PKCS#12(pfx)和PEM/DER檔案：

1. 將PKCS#7檔案轉換為臨時PEM檔案。

   要使用OpenSSL，請開啟「命令」窗口，然後輸入以下內容：

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >此臨時PEM包含您的證書和中間CA的證書。 使用這些證書生成PFX檔案。

1. 將臨時PEM檔案轉換為PFX檔案。

   要使用OpenSSL，請開啟「命令」窗口，然後輸入以下內容：

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. 將臨時PEM檔案轉換為最終PEM檔案。

   要使用OpenSSL，請開啟「命令」窗口，然後輸入以下內容：

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >雖然不是必需的，但Adobe建議為私鑰(privatekeypassword)和PFX(pfxpassword)使用不同的口令。

   此最終PEM檔案僅包含您的證書。

1. 將PEM檔案轉換為DER檔案。

   要使用OpenSSL，請開啟「命令」窗口，然後輸入以下內容：

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER檔案僅對HTTP Dynamic Streaming打包器是必需的。
