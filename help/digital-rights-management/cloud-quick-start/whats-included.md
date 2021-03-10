---
description: Adobe為不想開發和維護自己Primetime DRM License Server的Adobe PrimetimeDRM客戶提供雲DRM服務。 借由使用本服務，客戶可以降低DRM授權發行的操作和開發複雜性。 Primetime Cloud DRM可向所有能執行Primetime Browser TVSDK視訊應用程式（例如iOS、Android、桌上型電腦和Xbox360）的裝置發行DRM授權。 此DRM服務由Adobe代管和維護，全天候運作。
title: 背景
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 背景{#background}

Adobe為不想開發和維護自己Primetime DRM License Server的Adobe PrimetimeDRM客戶提供雲DRM服務。 借由使用本服務，客戶可以降低DRM授權發行的操作和開發複雜性。 Primetime Cloud DRM可向所有能執行Primetime Browser TVSDK視訊應用程式（例如iOS、Android、桌上型電腦和Xbox360）的裝置發行DRM授權。 此DRM服務由Adobe代管和維護，全天候運作。

>[!NOTE]
>
>Adobe PrimetimeDRM原名「Adobe存取」，在此之前稱為「Flash Access」。

## Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}包含哪些內容

* 自訂驗證／權益模組，以及如何針對您的內容使用自訂驗證的指示。 有關更多文檔，請參閱[!DNL Custom Authentication Entitlement]目錄。
* 雲端DRM專用的授權伺服器憑證([!DNL .pem/.cer/.der])

* 雲端DRM專用的授權伺服器傳輸憑證([!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* 打包的DRM策略示例

   * **policy_24hr** -許可證在磁碟上快取24小時。在24小時後，必須取得新的授權才能檢視內容。 此套件中的所有其他原則也有24小時的授權快取。
   * **policy_ios_remotekeyserver** -在iOS裝置上，將從Cloud DRM取得DRM授權。此外，客戶端將從雲DRM中獲取所有AES解密密鑰。 在中斷運作的iOS裝置上不允許播放。

   * **policy_ios_localkeyserver** -在iOS裝置上，將從Cloud DRM取得DRM授權。此外，用戶端將從本機HTTP伺服器取得所有HLS AES解密金鑰，而非雲端DRM。 在中斷運作的iOS裝置上不允許播放。

   * **policy_adobePass**  —— 用戶端必須先驗證(先前稱為Adobe Pass)，否則授權將被拒絕。

* Adobe策略管理器工具，用於建立其他DRM策略
* 用於封裝的範例視訊內容

