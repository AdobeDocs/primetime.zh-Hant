---
title: 生成證書籤名請求（請求者）
description: 生成證書籤名請求（請求者）
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# 生成證書籤名請求（請求者）{#generate-a-certificate-signing-request-requester}

1. 生成密鑰對。 要使用OpenSSL等實用程式，請開啟「命令窗口」並輸入以下內容：

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe建議在密鑰名中包括證書類型（lic、pkgr、trans、trial或eval）。 此命名慣例可讓您在授權伺服器上部署這些檔案更輕鬆。 此範例使用「mycompany-license.key」。 對於試用版和試用版，請使用「mycompany-eval.key」和「mycompany-trial.key」。

1. 輸入密碼以保護私密金鑰。

   密碼至少應包含12個字元。 字元應混合使用大寫和小寫ASCII字元和數字。 要使用OpenSSL生成強口令，請開啟命令窗口並輸入以下內容：

   ```
   openssl rand -base64 8
   ```

1. 產生憑證簽署要求(CSR)。

   要使用OpenSSL生成CSR，請開啟「命令窗口」並輸入以下內容：

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 系統會提示您輸入私密金鑰的密碼。
1. 建立您的私密金鑰和密碼的備份副本。

   如果您遺失私密金鑰或私密金鑰已洩露，請連絡Adobe憑證管理員以撤銷憑證並要求新的憑證。

   >[!NOTE]
   >
   >Adobe建議使用HSM來保護您的私密金鑰和密碼。

