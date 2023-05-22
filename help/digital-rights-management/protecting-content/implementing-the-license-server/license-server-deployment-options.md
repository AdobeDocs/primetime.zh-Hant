---
title: 許可證伺服器部署選項
description: 許可證伺服器部署選項
copied-description: true
exl-id: e06d59c0-517d-4483-9132-ceb37efada31
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 許可證伺服器部署選項{#license-server-deployment-options}

可以使用以下選項之一部署許可證伺服器：

* Adobe PrimetimeDRM伺服器，用於受保護的流處理 — 此許可證伺服器已針對流處理進行優化。 例如，您可以設定伺服器以使用Migniqe DRM進行AdobeHTTP Dynamic Streaming。 此伺服器可以輕鬆部署，只需很少的配置，並支援多個租戶。 它可以實現高級的可擴充性。 由於此實現針對流進行了優化，因此它不支援黃金時段DRM的全部功能。 例如，不支援用戶名/密碼驗證、域和許可證連結。 此伺服器頒發的許可證中的使用規則通過伺服器配置檔案控制，該檔案會覆蓋打包時使用的策略。

   查看 *Adobe PrimetimeDRM伺服器受保護流管理指南* 有關許可證伺服器支援的使用規則的詳細資訊。
* 參考實施許可證伺服器 — 您可以使用此設定來自定義伺服器實施。 這是一個許可證伺服器實現的示例，包括原始碼，它演示了如何使用Mighine DRM SDK中的API來管理所有類型的請求以及如何實現由資料庫支援的自定義業務邏輯。 此伺服器頒發的許可證中的使用規則通過與打包時的內容相關聯的策略進行控制。
* 自定義伺服器實施 — 您還可以使用SDK實施自己的許可伺服器。 該資訊描述了如何使用API來實現許可證伺服器。
