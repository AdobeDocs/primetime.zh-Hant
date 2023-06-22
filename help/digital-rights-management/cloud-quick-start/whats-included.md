---
description: Adobe提供雲端DRM服務給不想開發及維護自己的Primetime DRM授權伺服器的Adobe Primetime DRM客戶。 利用這項服務，客戶可以減少DRM授權發行相關的運作和開發複雜性。 Primetime Cloud DRM可以向所有能夠執行啟用Primetime瀏覽器TVSDK之視訊應用程式的裝置發放DRM授權，例如iOS、Android、桌上型電腦和Xbox360。 此DRM服務由Adobe託管及維護，全年無休運作。
title: 背景
exl-id: bb5ad080-5b1d-43a6-8d0e-9b5735c82d96
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 背景 {#background}

Adobe提供雲端DRM服務給不想開發及維護自己的Primetime DRM授權伺服器的Adobe Primetime DRM客戶。 利用這項服務，客戶可以減少DRM授權發行相關的運作和開發複雜性。 Primetime Cloud DRM可以向所有能夠執行啟用Primetime瀏覽器TVSDK之視訊應用程式的裝置發放DRM授權，例如iOS、Android、桌上型電腦和Xbox360。 此DRM服務由Adobe託管及維護，全年無休運作。

>[!NOTE]
>
>Adobe Primetime DRM先前稱為Adobe存取，之前稱為Flash Access。

## Primetime Cloud DRM包含哪些功能 {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* 自訂驗證/軟體權利檔案模組和如何參與內容自訂驗證的指示。 如需更多檔案，請參閱 [!DNL Custom Authentication Entitlement] 目錄。
* Cloud DRM專用授權伺服器憑證( [!DNL .pem/.cer/.der])

* 雲端DRM專屬授權伺服器傳輸憑證( [!DNL .pem/.cer/.der])

* Primetime Java離線封裝程式
* 封裝的DRM原則範例

   * **policy_24hr**  — 授權磁碟快取24小時。 24小時後，必須取得新授權才能檢視內容。 此套件中的所有其他原則也具有24小時授權快取。
   * **policy_ios_remotekeyserver**  — 在iOS裝置上，DRM授權將從Cloud DRM取得。 此外，使用者端會從Cloud DRM取得所有AES解密金鑰。 在遭監禁的iOS裝置上不允許播放。

   * **policy_ios_localkeyserver**  — 在iOS裝置上，DRM授權將從Cloud DRM取得。 此外，使用者端會從本機HTTP伺服器（而非雲端DRM）取得所有HLS AES解密金鑰。 在遭監禁的iOS裝置上不允許播放。

   * **policy_adobePass**  — 使用者端必須先使用(先前稱為Adobe Pass)進行驗證，否則授權會被拒絕。

* 建立其他DRM原則的Adobe原則管理員工具
* 封裝時使用的視訊內容範例
