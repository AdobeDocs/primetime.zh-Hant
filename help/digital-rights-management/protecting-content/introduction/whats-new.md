---
description: Adobe PrimetimeDRM是高價值視聽內容的先進Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Primetime DRM SDK來指定DRM原則、將這些原則套用至內容，以及加密該內容。
title: Adobe PrimetimeDRM的新增功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Adobe PrimetimeDRM的新增功能{#what-is-new-in-adobe-primetime-drm}

Adobe PrimetimeDRM是高價值視聽內容的先進Digital Rights Management(DRM)和內容保護解決方案。 在支援建立Java API的應用程式中，您可以使用Primetime DRM SDK來指定DRM原則、將這些原則套用至內容，以及加密該內容。

>[!NOTE]
>
>Primetime DRM先前稱為「Adobe存取」，在之前稱為「Flash Access」。

以下是內容保護流程的高級逐步介紹：

1. 使用DRM Java API設定DRM策略屬性和加密參數。
1. 建立描述任何內容之使用角色的DRM原則。

   您可以建立任意數量的DRM策略。 大多數用戶建立少量策略，然後將它們應用到多個檔案。
1. 封裝媒體檔案。

   *`Packaging a file`* 意指您加密檔案，然後套用DRM原則至檔案。
1. 實作授權伺服器，以向使用者發放授權。

完成這些步驟後，您的加密內容就可供部署。 在部署後，用戶端可向授權伺服器要求授權，而收到後可播放內容。

Primetime DRM SDK提供Java API來完成這些工作。 SDK包括授權伺服器和命令列工具的參考實作，兩者皆以DRM SDK Java API為基礎。

以下說明的功能是此版本的新功能。

## 新功能{#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **硬停止-** 您可以指定在播放窗口的末尾停止或繼續播放。
* **與解析度相關的輸出控制-** 您可以根據像素解析度指定輸出約束。
* **授權伺服器回應匿名化-** 為了使用Primetime DRM授權伺服器通訊協定來增強隱私權，傳輸憑證序號將會設為授權伺服器回應支援用戶端的零位。

