---
seo-title: 續約憑證
title: 續約憑證
uuid: 12a560b0-966b-424e-bfe5-22e9c10d8667
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 續約憑證{#renew-certificates}

您應注意以下憑證續約限制，這些限制是根據您的Adobe Primetime DRM SDK設定：

* Primetime DRM Production SDK

   當您購買支援合約時，Adobe會提供Primetime DRM Production SDK的初始一組免費憑證。 如果您沒有支援合約，則可購買一組有效期為兩年的續約憑證。
* Primetime DRM評估SDK

   本SDK的憑證集有效期為一年，無法續約。
* Primetime DRM試用版SDK

   Primetime DRM試用版SDK的有效期為三個月，而Adobe提供一套免費續約憑證。

## 實作新憑證並使用舊憑證來建立現有內容 {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

在Primetime DRM中，您可以允許授權伺服器針對與先前（甚至過期）封裝器憑證一起封裝的內容核發授權。 若要設定您的伺服器接受先前封裝內容的授權要求，請將您的舊憑證提供給您的伺服器，並更新您的伺服器組態檔，讓伺服器知道在何處尋找舊憑證。 如需詳細資訊，請參 *閱「使用Adobe Primetime DRM SDK for Protecting Content* 」中 *的「當Adobe核發的憑證到期時處理憑證更新」*。

如果您的伺服器應用程式是以Primetime DRM參考實作為基礎，則不需要更新伺服器端程式。 在檔案 `flashaccess-refimpl.properties` 中，有一些欄位可以在其中指定其他傳輸和許可證伺服器證書。 如果您只有一個憑證，則不需要填入這些屬性。 如果您已過期的憑證，而且想在您發出授權回應時使用這些憑證，則必須將這些憑證提供至設定檔案並重新啟動伺服器。

若要指定舊憑證，請使用下列屬性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

