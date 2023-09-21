---
title: 產生憑證簽署要求（請求者）
description: 產生憑證簽署要求（請求者）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 產生憑證簽署要求（請求者） {#generate-a-certificate-signing-request-requester}

1. 產生金鑰組。 若要使用OpenSSL等公用程式，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe建議在金鑰名稱中包含憑證型別（lic、pkgr、trans、trial或eval）。 此命名慣例可讓您在授權伺服器上部署這些裝置時更輕鬆。 此範例使用「mycompany-license.key」。 評估版和試用版請使用「mycompany-eval.key」和「mycompany-trial.key」。

1. 輸入密碼以保護私密金鑰。

   密碼應至少包含12個字元。 字元應混合使用大寫和小寫ASCII字元和數字。 若要使用OpenSSL來產生強式密碼，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl rand -base64 8
   ```

1. 產生憑證申請檔(CSR)。

   若要使用OpenSSL來產生CSR，請開啟「命令視窗」並輸入下列內容：

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 系統會提示您輸入私密金鑰的密碼。
1. 建立您的私密金鑰和密碼的備份復本。

   如果您遺失私密金鑰或金鑰遭到破壞，請聯絡Adobe憑證管理員以撤銷您的憑證並索取新憑證。

   >[!NOTE]
   >
   >Adobe建議使用HSM來保護您的私密金鑰和密碼。
