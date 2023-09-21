---
title: 在Adobe發行的憑證過期時處理憑證更新
description: 在Adobe發行的憑證過期時處理憑證更新
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 在Adobe發行的憑證過期時處理憑證更新{#handling-certificate-updates-when-adobe-issued-certificates-expire}

您可能需要從Adobe取得新憑證。 例如，生產憑證會在評估憑證過期或您從評估切換至生產憑證時過期。 當憑證過期且您不想重新封裝使用舊憑證的內容時，您可以讓License Server知道舊憑證和新憑證。

若要使用新憑證更新伺服器：

1. （選擇性）當您將新專案新增至現有DRM原則更新清單或撤銷清單時，您需要使用新憑證進行簽署，並使用舊憑證來驗證現有檔案上的簽章。

   例如，您可以使用下列命令列，將專案加入已使用不同認證簽署的現有DRM原則更新清單：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. （可選）使用Java API以新的DRM原則更新清單或撤銷清單來更新授權伺服器：

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實作中，您使用的屬性為 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`. 您也需要更新用來驗證簽章的憑證： `RevocationList.verifySignature.X509Certificate`.

1. 使用新憑證和舊憑證更新授權伺服器。

   如果您要使用已使用舊憑證封裝的內容，請確定授權伺服器可存取舊和新的授權伺服器憑證以及傳輸憑證。

   對於授權伺服器認證：

   * 請確認目前的認證已傳遞至 `LicenseHandler` 建構函式：

      * 在參考實作中，使用 `LicenseHandler.ServerCredential` 屬性。
      * 在Adobe Primetime DRM Server for Protected Streaming中，目前的認證必須是在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。

   * 確保提供目前和舊認證給 `AsymmetricKeyRetrieval`

      * 在參考實作中，使用 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 屬性。

      * 在Primetime DRM Server for Protected Streaming中，舊認證是在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。

   對於傳輸認證：

   * 請確認目前的認證已傳遞至 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在參考實作中，使用 `HandlerConfiguration.ServerTransportCredential` 屬性。
      * 在用於受保護串流的Primetime DRM伺服器中，目前的認證必須是中指定的第一個認證 `TransportCredential` 中的元素 [!DNL flashaccess-tenant.xml] 檔案。

   * 確保提供舊憑證給 `HandlerConfiguration.setAdditionalServerTransportCredentials`()：

      * 在參考實作中，使用 `HandlerConfiguration.AdditionalServerTransportCredential. n` 屬性。
      * 在用於受保護串流的Primetime DRM伺服器中，這會在中的第一個認證之後指定 `TransportCredential` flashaccess-tenant.xml檔案中的元素。

1. 更新封裝工具，確保使用目前的認證來封裝內容。 確保封裝時使用最新的授權伺服器憑證、傳輸憑證和封裝者認證。
1. 更新金鑰伺服器的授權伺服器憑證，如下所示：

   * 在Adobe Primetime DRM Key Server租使用者組態檔中更新認證，方法是在flashaccess-keyserver-tenant.xml中加入舊和新的Key Server認證。
   * 確定目前的憑證已傳遞至 `HandlerConfiguration.setKeyServerCertificate()` 方法。

      * 在參考實作中，使用 `HandlerConfiguration.KeyServerCertificate` 屬性。
      * 在Primetime DRM Server for Protected Streaming中，透過Configuration/Tenant/Certificates/KeyServer元素在中指定金鑰伺服器的憑證。
