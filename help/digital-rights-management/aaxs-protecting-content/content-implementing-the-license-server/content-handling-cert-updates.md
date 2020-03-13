---
seo-title: 當您的Adobe核發憑證到期時，處理憑證更新
title: 當您的Adobe核發憑證到期時，處理憑證更新
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 當您的Adobe核發憑證到期時，處理憑證更新 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

有時候，您可能必須向Adobe取得新憑證。 例如，當生產憑證過期時，評估憑證會過期，或者當您從評估切換到生產憑證時。 當憑證過期，而您不想重新封裝使用舊憑證的內容時。 您可讓授權伺服器同時瞭解舊憑證和新憑證。

使用下列步驟使用新證書更新伺服器：

1. （選擇性）在將新項目新增至現有的原則更新清單或撤銷清單時，請務必使用新認證進行簽署，並使用舊憑證來驗證現有檔案的簽名。

   例如，使用以下命令行將條目添加到使用不同憑據簽名的現有策略更新清單中：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. 使用Java API以新的原則更新清單或撤銷清單來更新授權伺服器：

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實作中，您使用的屬性是 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 此外，也請更新用於驗證簽名的憑證： `RevocationList.verifySignature.X509Certificate`。

1. 若要使用使用舊證書打包的內容，許可證伺服器需要新舊許可證伺服器證書和傳輸證書。 使用新舊憑證更新授權伺服器。

   對於許可證伺服器憑據：

   * 請確定目前的憑證已傳遞至建構 `LicenseHandler` 函式：

      * 在參考實作中，透過屬性設定 `LicenseHandler.ServerCredential` 它。
      * 在Adobe Access Server for Protected Streaming中，目前的憑證必須是flashaccess-tenant.xml檔案中元素中指 `LicenseServerCredential` 定的第一個憑證。
   * 請確定目前和舊的認證已提供給 `AsymmetricKeyRetrieval`

      * 在參考實作中，透過和屬性設 `LicenseHandler.ServerCredential` 定 `AsymmetricKeyRetrieval.ServerCredential. n` 它。
      * 在Adobe Access Server for Protected Streaming中，舊認證是在flashaccess-tenant.xml檔案中的元素中 `LicenseServerCredential` 第一個憑證之後指定。
   對於傳輸憑據：

   * 確保將當前憑據傳遞到方 `HandlerConfiguration.setServerTransportCredential()` 法：

      * 在參考實作中，透過屬性設定 `HandlerConfiguration.ServerTransportCredential` 它。
      * 在Adobe Access Server中，針對受保護的串流，目前的憑證必須是flashaccess-tenant.xml檔案中 `TransportCredential` 元素中指定的第一個憑證。
   * 請確定舊憑證已提供 `HandlerConfiguration.setAdditionalServerTransportCredentials`給():

      * 在參考實作中，透過屬性設定 `HandlerConfiguration.AdditionalServerTransportCredential. n` 它。
      * 在Adobe Access Server中，受保護的串流，這是在flashaccess-tenant.xml檔案中元素中的 `TransportCredential` 第一個憑證之後指定。




1. 更新封裝工具，以確定其是使用目前的認證封裝內容。 請確定封裝時使用最新的授權伺服器憑證、傳輸憑證和封裝憑證。
1. 要更新密鑰伺服器的許可證伺服器證書，請執行以下操作：

   * 更新Adobe Access Key Server租用戶設定檔案中的認證。 在flashaccess-keyserver-tenant.xml中同時包含舊版和新版Key Server憑證。
   * 請確定目前的憑證已傳入方 `HandlerConfiguration.setKeyServerCertificate()` 法。

      * 在參考實作中，透過屬性設定 `HandlerConfiguration.KeyServerCertificate` 它。
      * 在Adobe Access Server的受保護串流中，透過Configuration/Tenant/Certificates/KeyServer元素，指定Key Server的憑證。

