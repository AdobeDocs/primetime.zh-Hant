---
title: 續約憑證
description: 續約憑證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# 續約憑證{#renew-certificates}

您應注意以下憑證續約限制，這些限制是以您的Adobe PrimetimeDRM SDK組態為基礎：

* Primetime DRM Production SDK

   Adobe在您購買支援合約時，提供Primetime DRM Production SDK的初始一組免費憑證。 如果您沒有支援合約，則可購買一組有效期為兩年的續約憑證。
* Primetime DRM評估SDK

   本SDK的憑證集有效期為一年，無法續約。
* Primetime DRM試用版SDK

   Primetime DRM試用版SDK的有效期為三個月，而Adobe則提供一套免費續約憑證。

## 實作新憑證並使用舊憑證來處理現有內容{#section_345C92D1C9794B0BBB9A9B0702EC95FF}

在Primetime DRM中，您可以允許授權伺服器針對與先前（甚至過期）封裝器憑證一起封裝的內容核發授權。 若要設定您的伺服器接受先前封裝內容的授權要求，請將您的舊憑證提供給您的伺服器，並更新您的伺服器組態檔，讓伺服器知道在何處尋找舊憑證。 如需詳細資訊，請參閱&#x200B;*使用Adobe PrimetimeDRM SDK保護內容*&#x200B;中的&#x200B;*當Adobe核發的憑證到期時處理憑證更新。*

如果您的伺服器應用程式是以Primetime DRM參考實作為基礎，則不需要更新伺服器端程式。 在`flashaccess-refimpl.properties`檔案中，有欄位可指定其他傳輸和授權伺服器憑證。 如果您只有一個憑證，則不需要填入這些屬性。 如果您已過期的憑證，而且想在您發出授權回應時使用這些憑證，則必須將這些憑證提供至設定檔案並重新啟動伺服器。

若要指定舊憑證，請使用下列屬性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

