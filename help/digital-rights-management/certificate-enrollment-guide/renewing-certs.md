---
title: 續訂證書
description: 續訂證書
copied-description: true
exl-id: db130ca5-4e26-447f-b2f4-4eee0838fd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 續訂證書{#renew-certificates}

您應瞭解基於Adobe PrimetimeDRM SDK配置的以下證書續訂限制：

* 黃金時段DRM製作SDK

   Adobe在您購買支援合同時為Mogine DRM Production SDK提供初始的一組免費證書。 如果您沒有支援合同，則可以購買一組有效期為兩年的續訂證書。
* 黃金時段DRM評估SDK

   此SDK的證書集的有效期為一年，無法續訂。
* 黃金時段DRM試用版SDK

   黃金時段DRM試用版SDK有效期為三個月，Adobe提供一組免費續訂證書。

## 為現有內容實施新證書和使用舊證書 {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

在黃金時段DRM中，您可以允許許可證伺服器為與先前（甚至過期）打包器證書打包的內容頒發許可證。 要配置伺服器以接受來自以前打包內容的許可證請求，請將舊證書提供到伺服器並更新伺服器的配置檔案，以便伺服器知道在何處查找舊證書。 有關詳細資訊，請參見 *在Adobe頒發的證書過期時處理證書更新* 在 *使用Adobe PrimetimeDRM SDK保護內容*。

如果您的伺服器應用程式基於黃金時段DRM參考實現，則無需更新您的伺服器端程式。 在 `flashaccess-refimpl.properties` 檔案中，您可以在其中指定其他傳輸和許可證伺服器證書。 如果您只有一個證書，則不必填充這些屬性。 如果證書已過期，並且希望在發出許可證響應時使用這些證書，則必須向配置檔案提供這些證書並重新啟動伺服器。

要指定舊證書，請使用以下屬性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
