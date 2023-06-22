---
title: 授權伺服器部署選項
description: 授權伺服器部署選項
copied-description: true
exl-id: e06d59c0-517d-4483-9132-ceb37efada31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 授權伺服器部署選項{#license-server-deployment-options}

您可以使用下列其中一個選項來部署License Server：

* 適用於受保護串流的Adobe Primetime DRM伺服器 — 此授權伺服器已針對串流最佳化。 例如，您可以設定伺服器以使用Primetime DRM進行AdobeHTTP Dynamic Streaming。 此伺服器可輕鬆部署，幾乎不需要任何設定，並支援多個租使用者。 它可達到高水準的擴充性。 由於此實作已針對串流最佳化，因此不支援完整的Primetime DRM功能。 例如，不支援使用者名稱/密碼驗證、網域和授權鏈結。 此伺服器所核發的授權中的使用規則，是由伺服器設定檔所控制，該設定檔會覆寫封裝時所使用的原則。

   請參閱 *Adobe Primetime DRM Server for Protected Streaming指南* 瞭解授權伺服器支援的使用規則詳細資訊。
* Reference Implementation License Server — 您可以使用此設定來自訂伺服器實作。 這是授權伺服器實作的範例，包括原始程式碼，示範如何使用Primetime DRM SDK中的API來管理所有型別的請求，以及如何實作資料庫支援的自訂商業邏輯。 此伺服器所核發的授權中的使用規則，是由封裝時與內容相關的原則所控制。
* 自訂伺服器實作 — 您也可以使用SDK實作自己的授權伺服器。 此資訊說明如何使用API來實作授權伺服器。
