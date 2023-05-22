---
title: 在Adobe頒發的證書過期時處理證書更新
description: 在Adobe頒發的證書過期時處理證書更新
copied-description: true
exl-id: 9768544e-7e92-4c3a-9863-af9aed74a0c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# 在Adobe頒發的證書過期時處理證書更新 {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

有時候你必須從Adobe獲得新證書。 例如，當生產證書過期時，評估證書過期，或者從評估切換到生產證書時。 當證書過期且您不想重新打包使用舊證書的內容時。 您可以使許可證伺服器瞭解舊證書和新證書。

請按下列步驟使用新證書更新伺服器：

1. （可選）在將新條目添加到現有策略更新清單或吊銷清單時，請確保使用新憑據簽名，並使用舊證書驗證現有檔案上的簽名。

   例如，使用以下命令行向使用其他憑據簽名的現有策略更新清單中添加一個條目：

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. 使用Java API使用新策略更新清單或吊銷清單更新許可證伺服器：

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   或：

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   在參考實現中，您使用的屬性是 `HandlerConfiguration.RevocationList` 和 `HandlerConfiguration.PolicyUpdateList`。 還更新用於驗證簽名的證書： `RevocationList.verifySignature.X509Certificate`。

1. 要使用使用舊證書打包的內容，許可證伺服器需要舊和新許可證伺服器憑據以及傳輸憑據。 使用新證書和舊證書更新許可證伺服器。

   對於許可證伺服器憑據：

   * 確保將當前憑據傳入 `LicenseHandler` 建構子：

      * 在參考實現中，通過 `LicenseHandler.ServerCredential` 屬性。
      * 在Adobe Access Server的受保護流中，當前憑據必須是在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   * 確保向提供當前和舊憑據 `AsymmetricKeyRetrieval`

      * 在參考實現中，通過 `LicenseHandler.ServerCredential` 和 `AsymmetricKeyRetrieval.ServerCredential. n` 屬性。
      * 在Adobe Access Server的受保護流管理中，舊憑據在 `LicenseServerCredential` flashaccess-tenant.xml檔案中的元素。
   對於傳輸憑據：

   * 確保將當前憑據傳入 `HandlerConfiguration.setServerTransportCredential()` 方法：

      * 在參考實現中，通過 `HandlerConfiguration.ServerTransportCredential` 屬性。
      * 在Adobe Access Server中，當前憑據必須是在 `TransportCredential` flashaccess-tenant.xml檔案中的元素。
   * 確保向提供舊憑據 `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * 在參考實現中，通過 `HandlerConfiguration.AdditionalServerTransportCredential. n` 屬性。
      * 在受保護的流式傳輸的Adobe Access Server中，這是在 `TransportCredential` flashaccess-tenant.xml檔案中的元素。




1. 更新打包工具，以確保它們使用當前憑據打包內容。 確保使用最新的許可證伺服器證書、傳輸證書和打包器憑據進行打包。
1. 要更新密鑰伺服器的許可證伺服器證書：

   * 更新Adobe訪問密鑰伺服器租戶配置檔案中的憑據。 在flashaccess-keyserver-tenant.xml中同時包括舊密鑰伺服器憑據和新密鑰伺服器憑據。
   * 確保將當前證書傳遞到 `HandlerConfiguration.setKeyServerCertificate()` 的雙曲餘切值。

      * 在參考實現中，通過 `HandlerConfiguration.KeyServerCertificate` 屬性。
      * 在「受保護的流」的Adobe Access Server中，通過Configuration/Tenant/Certificates/KeyServer元素在中指定密鑰伺服器的證書。
