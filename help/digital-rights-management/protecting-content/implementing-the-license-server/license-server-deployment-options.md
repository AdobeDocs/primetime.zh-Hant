---
title: 授權伺服器部署選項
description: 授權伺服器部署選項
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# 許可證伺服器部署選項{#license-server-deployment-options}

您可以使用下列其中一個選項來部署授權伺服器：

* Adobe Primetime保護串流的DRM伺服器——此授權伺服器已針對串流最佳化。 例如，您可以設定伺服器，以便使用Primetime DRM進行AdobeHTTP Dynamic Streaming。 此伺服器可輕鬆部署，只需極少的組態，並支援多個租戶。 它可以實現高級別的可擴充性。 由於此實作已針對串流最佳化，因此不支援完整的Primetime DRM功能。 例如，使用者名稱／密碼驗證、網域和授權鏈結不受支援。 此伺服器所核發之授權中的使用規則會透過伺服器組態檔加以控制，而此組態檔會覆寫封裝時使用的原則。

   請參閱&#x200B;*《Adobe PrimetimeDRM Server for Protected Streaming Guide》（保護串流版DRM伺服器指南），以取得授權伺服器支援之使用規則的詳細資訊。*
* 參考實作授權伺服器——您可使用此設定來自訂您的伺服器實作。 這是授權伺服器實作的範例，包括原始碼，它示範如何使用Primetime DRM SDK中的API來管理所有類型的請求，以及如何實作由資料庫支援的自訂商業邏輯。 此伺服器所核發之授權中的使用規則，是透過封裝時與內容相關的原則加以控制。
* 自訂伺服器實作——您也可以使用SDK實作您自己的授權伺服器。 這些資訊說明如何使用API來實作授權伺服器。

