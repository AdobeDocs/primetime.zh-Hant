---
title: 更新憑證
description: 更新憑證
copied-description: true
exl-id: db130ca5-4e26-447f-b2f4-4eee0838fd56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 更新憑證{#renew-certificates}

請注意以下根據您Adobe Primetime DRM SDK設定的憑證續約限制：

* Primetime DRM Production SDK

   當您購買支援合約時，Adobe會為Primetime DRM Production SDK提供初始的免費憑證集。 如果您沒有支援合約，您可以購買一組有效期為兩年的續約憑證。
* Primetime DRM評估SDK

   此SDK的憑證集有效期為一年，無法續約。
* Primetime DRM試用版SDK

   Primetime DRM試用版SDK的有效期為三個月，而Adobe則提供一組免費的續約憑證。

## 實作新憑證並對現有內容使用舊憑證 {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

在Primetime DRM中，您可以允許授權伺服器為使用先前封裝器憑證（甚至過期）封裝的內容發行授權。 若要設定您的伺服器以接受來自先前封裝內容的授權要求，請將您的舊憑證提供給伺服器並更新伺服器的設定檔案，讓伺服器知道在哪裡可以找到舊憑證。 如需詳細資訊，請參閱 *在Adobe發行的憑證過期時處理憑證更新* 在 *使用Adobe Primetime DRM SDK保護內容*.

如果您的伺服器應用程式是以Primetime DRM Reference Implementation為基礎，則不必更新伺服器端程式。 在 `flashaccess-refimpl.properties` 檔案中，有些欄位可讓您指定其他傳輸和授權伺服器憑證。 如果您只有一個憑證，則不需要填入這些屬性。 如果您有過期的憑證，並且想要在發行授權回應時使用這些憑證，則必須將這些憑證提供給設定檔案並重新啟動伺服器。

若要指定舊憑證，請使用下列屬性：

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
