---
seo-title: 在Adobe核發的憑證到期時處理憑證更新
title: 在Adobe核發的憑證到期時處理憑證更新
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 在Adobe核發的憑證到期時處理憑證更新{#handling-certificate-updates-when-adobe-issued-certificates-expire}

您可能需要向Adobe取得新的憑證。 例如，當評估憑證過期或從評估憑證切換至生產憑證時，生產憑證會過期。 每當憑證過期且您不想重新封裝使用舊憑證的內容時，您就可讓授權伺服器同時知道舊憑證和新憑證。

要使用新證書更新伺服器：

1. （可選）當您將新項目新增至現有DRM原則更新清單或撤銷清單時，您必須使用新認證並使用舊認證來驗證現有檔案的簽名。

   例如，您可以使用以下命令行將條目添加到已使用不同憑據簽名的現有DRM策略更新清單：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. （選擇性）使用Java API以新的DRM政策更新清單或撤銷清單來更新授權伺服器：

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實施中，您使用的屬性是 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 您還需要更新用於驗證簽名的證書： `RevocationList.verifySignature.X509Certificate`。

1. 使用新舊憑證更新授權伺服器。

   如果您想要使用使用舊證書打包的內容，請確保許可證伺服器可以訪問新舊許可證伺服器憑據以及傳輸憑據。

   對於許可證伺服器憑據：

   * 請確定目前的憑證已傳遞至建構 `LicenseHandler` 函式：

      * 在參考實作中，使用屬性設定 `LicenseHandler.ServerCredential` 它。
      * 在Adobe Primetime DRM Server for Protected Streaming中，目前的憑證必須是flashaccess-tenant.xml檔案中元素中指 `LicenseServerCredential` 定的第一個憑證。
   * 請確定目前和舊的認證已提供給 `AsymmetricKeyRetrieval`

      * 在參考實作中，使用和屬性設 `LicenseHandler.ServerCredential` 定 `AsymmetricKeyRetrieval.ServerCredential. n` 它。

      * 在Primetime DRM Server for Protected Streaming中，舊憑證是在flashaccess-tenant.xml檔案中的元素中的第 `LicenseServerCredential` 一個憑證之後指定。
   對於傳輸憑據：

   * 確保將當前憑據傳遞到方 `HandlerConfiguration.setServerTransportCredential()` 法：

      * 在參考實作中，使用屬性設定 `HandlerConfiguration.ServerTransportCredential` 它。
      * 在用於受保護串流的Primetime DRM伺服器中，目前的憑證必須是檔案中元素中指 `TransportCredential` 定的第一個憑 [!DNL flashaccess-tenant.xml] 證。
   * 請確定舊憑證已提供 `HandlerConfiguration.setAdditionalServerTransportCredentials`給():

      * 在參考實作中，使用屬性設定 `HandlerConfiguration.AdditionalServerTransportCredential. n` 它。
      * 在Primetime DRM Server中，保護串流的這個指定是在flashaccess-tenant.xml檔案中 `TransportCredential` 元素的第一個憑證之後。




1. 更新封裝工具，以確定其是使用目前的認證封裝內容。 請確定封裝時使用最新的授權伺服器憑證、傳輸憑證和封裝憑證。
1. 按如下方式更新密鑰伺服器的許可證伺服器證書：

   * 在Flashaccess-keyserver-tenant.xml中加入舊的和新的Key Server憑證，以更新Adobe Primetime DRM Key Server租用戶設定檔中的憑證。
   * 請確定目前的憑證已傳遞至 `HandlerConfiguration.setKeyServerCertificate()` 方法。

      * 在參考實作中，使用屬性設定 `HandlerConfiguration.KeyServerCertificate` 它。
      * 在用於受保護流的Primetime DRM伺服器中，通過Configuration/Tenant/Certificates/KeyServer元素在中指定Key Server的證書。

