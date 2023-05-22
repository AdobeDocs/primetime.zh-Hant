---
title: 在Adobe頒發的證書過期時處理證書更新
description: 在Adobe頒發的證書過期時處理證書更新
copied-description: true
exl-id: 9051a647-87ed-4df6-8bbc-bb5c112383ee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 在Adobe頒發的證書過期時處理證書更新{#handling-certificate-updates-when-adobe-issued-certificates-expire}

您可能需要從Adobe獲取新證書。 例如，當評估證書過期或從評估切換到生產證書時，生產證書將過期。 無論何時證書過期，並且您不想重新打包使用舊證書的內容，您都可以使許可證伺服器知道舊證書和新證書。

使用新證書更新伺服器：

1. （可選）在將新條目添加到現有DRM策略更新清單或吊銷清單時，需要使用新憑據簽名並使用舊證書驗證現有檔案上的簽名。

   例如，可以使用以下命令行將條目添加到已使用其他憑據簽名的現有DRM策略更新清單：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. （可選）使用Java API使用新的DRM策略更新清單或吊銷清單更新許可證伺服器：

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實現中，您使用的屬性 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 您還需要更新用於驗證簽名的證書： `RevocationList.verifySignature.X509Certificate`。

1. 使用新證書和舊證書更新許可證伺服器。

   如果要使用使用舊證書打包的內容，請確保許可證伺服器有權訪問舊和新許可證伺服器憑據以及傳輸憑據。

   對於許可證伺服器憑據：

   * 確保將當前憑據傳遞給 `LicenseHandler` 建構子：

      * 在參考實現中，將其設定為 `LicenseHandler.ServerCredential` 屬性。
      * 在Adobe PrimetimeDRM Server中，當前憑據必須是在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   * 確保向提供當前和舊憑據 `AsymmetricKeyRetrieval`

      * 在參考實現中，將其設定為 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 屬性。

      * 在用於受保護流的黃金時段DRM伺服器中，舊憑據在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   對於傳輸憑據：

   * 確保將當前憑據傳遞給 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在參考實現中，將其設定為 `HandlerConfiguration.ServerTransportCredential` 屬性。
      * 在用於受保護流的黃金時段DRM伺服器中，當前憑據必須是在 `TransportCredential` 元素 [!DNL flashaccess-tenant.xml] 的子菜單。
   * 確保向提供舊憑據 `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * 在參考實現中，將其設定為 `HandlerConfiguration.AdditionalServerTransportCredential. n` 屬性。
      * 在用於受保護流的黃金時段DRM伺服器中，這是在 `TransportCredential` flashaccess-tenant.xml檔案中的元素。




1. 更新打包工具，以確保它們正在將內容與當前憑據打包。 確保使用最新的許可證伺服器證書、傳輸證書和打包器憑據進行打包。
1. 按如下方式更新密鑰伺服器的許可證伺服器證書：

   * 通過在flashaccess-keyserver-tenant.xml中同時包含舊密鑰伺服器憑據和新密鑰伺服器憑據，更新Adobe PrimetimeDRM密鑰伺服器租戶配置檔案中的憑據。
   * 確保將當前證書傳遞到 `HandlerConfiguration.setKeyServerCertificate()` 的雙曲餘切值。

      * 在參考實現中，將其設定為 `HandlerConfiguration.KeyServerCertificate` 屬性。
      * 在用於受保護流的黃金時段DRM伺服器中，通過Configuration/Tenant/Certificates/KeyServer元素在中指定密鑰伺服器的證書。
