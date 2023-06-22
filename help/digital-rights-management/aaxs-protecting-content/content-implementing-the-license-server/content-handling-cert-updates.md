---
title: 在Adobe核發的憑證過期時處理憑證更新
description: 在Adobe核發的憑證過期時處理憑證更新
copied-description: true
exl-id: 9768544e-7e92-4c3a-9863-af9aed74a0c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# 在Adobe核發的憑證過期時處理憑證更新 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

有時候，您可能必須從Adobe取得新憑證。 例如，當生產憑證過期時、評估憑證過期時，或當您從評估切換至生產憑證時。 憑證過期時，而您不想重新封裝使用舊憑證的內容。 您可以讓License Server知道舊憑證和新憑證。

使用以下程式，以新憑證更新您的伺服器：

1. （選擇性）將新專案新增至現有原則更新清單或撤銷清單時，請務必使用新憑證簽署，並使用舊憑證來驗證現有檔案上的簽章。

   例如，使用以下命令列，將專案新增至使用不同認證簽署的現有原則更新清單：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. 使用Java API以新的原則更新清單或撤銷清單更新授權伺服器：

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實作中，您使用的屬性為 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`. 同時更新用來驗證簽章的憑證： `RevocationList.verifySignature.X509Certificate`.

1. 若要使用使用使用舊憑證封裝的內容，授權伺服器需要舊和新的授權伺服器憑證及傳輸憑證。 使用新憑證和舊憑證更新授權伺服器。

   對於授權伺服器認證：

   * 確保目前的認證已傳遞至 `LicenseHandler` 建構函式：

      * 在參考實作中，透過 `LicenseHandler.ServerCredential` 屬性。
      * 在Adobe Access Server for Protected Streaming中，目前的認證必須是 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   * 確保提供目前和舊認證給 `AsymmetricKeyRetrieval`

      * 在參考實作中，透過 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 屬性。
      * 在Adobe Access Server for Protected Streaming中，舊認證是在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   對於傳輸認證：

   * 確保目前的認證已傳遞至 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在參考實作中，透過 `HandlerConfiguration.ServerTransportCredential` 屬性。
      * 在用於受保護串流的Adobe Access Server中，目前的認證必須是中指定的第一個認證 `TransportCredential` flashaccess-tenant.xml檔案中的元素。
   * 確保提供舊認證給 `HandlerConfiguration.setAdditionalServerTransportCredentials`()：

      * 在參考實作中，透過 `HandlerConfiguration.AdditionalServerTransportCredential. n` 屬性。
      * 在適用於受保護串流的Adobe Access Server中，這會在中的第一個認證之後指定 `TransportCredential` flashaccess-tenant.xml檔案中的元素。




1. 更新封裝工具，確保它們使用目前的憑證封裝內容。 確保封裝時使用最新的授權伺服器憑證、傳輸憑證和封裝程式認證。
1. 若要更新金鑰伺服器的授權伺服器憑證：

   * 更新Adobe存取金鑰伺服器租使用者設定檔案中的認證。 在flashaccess-keyserver-tenant.xml中同時包含舊金鑰伺服器認證和新Key Server認證。
   * 確保目前的憑證已傳遞至 `HandlerConfiguration.setKeyServerCertificate()` 方法。

      * 在參考實作中，透過 `HandlerConfiguration.KeyServerCertificate` 屬性。
      * 在適用於受保護串流的Adobe Access Server中，透過Configuration/Tenant/Certificates/KeyServer元素在中指定金鑰伺服器的憑證。
