---
title: 生成證書籤名請求（請求者）
description: 生成證書籤名請求（請求者）
copied-description: true
exl-id: 4f8dae3d-da56-453d-b3c4-e67fe4f37064
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 生成證書籤名請求（請求者） {#generate-a-certificate-signing-request-requester}

1. 生成密鑰對。 要使用OpenSSL等實用程式，請開啟「命令窗口」，然後輸入以下內容：

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe建議在密鑰名中包括證書類型（lic、pkgr、trans、trial或eval）。 此命名約定使您在許可證伺服器上部署它們時更輕鬆。 此示例使用&quot;mycompany-license.key&quot;。 對於評估版和試用版，請使用「mycompany-eval.key」和「mycompany-trial.key」。

1. 輸入密碼以保護私鑰。

   密碼應至少包含12個字元。 字元應包括大寫和小寫ASCII字元和數字的混合。 要使用OpenSSL生成強密碼，請開啟命令窗口並輸入以下內容：

   ```
   openssl rand -base64 8
   ```

1. 生成證書籤名請求(CSR)。

   要使用OpenSSL生成CSR，請開啟「命令窗口」，然後輸入以下內容：

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. 系統將提示您輸入私鑰的密碼。
1. 建立私鑰和密碼的備份副本。

   如果您丟失了私鑰或私鑰被洩露，請與Adobe證書管理員聯繫以撤消您的證書並請求新證書。

   >[!NOTE]
   >
   >Adobe建議使用HSM保護您的私鑰和密碼。
