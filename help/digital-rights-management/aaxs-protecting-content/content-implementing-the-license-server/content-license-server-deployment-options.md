---
title: 許可證伺服器部署選項
description: 許可證伺服器部署選項
copied-description: true
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 許可證伺服器部署選項{#license-server-deployment-options}

可以使用以下選項之一部署許可證伺服器：

* **Adobe Access Server用於受保護的流式處理**  — 此許可證伺服器已針對流進行優化。 例如，您可以設定伺服器以使用Adobe訪問HTTP Dynamic Streaming。 此伺服器可以輕鬆部署，所需配置非常少，可支援多個租戶，並可實現高級別的可擴充性。 但是，由於此實施針對流進行了優化，因此它不支援完整的Adobe訪問功能。 例如，不支援用戶名/密碼驗證、域和許可證連結。 此伺服器頒發的許可證中的使用規則通過伺服器配置檔案控制，該檔案會覆蓋打包時使用的策略。 查看 *Adobe Access Server的受保護流管理指南* 有關此伺服器支援的使用規則的詳細資訊。
* **參考實施許可證伺服器**  — 將此設定用作自定義伺服器實現的起點。 這是一個許可證伺服器實現的示例，包括原始碼，它演示了如何使用Adobe訪問SDK中的API來處理所有類型的請求以及如何實現由資料庫支援的自定義業務邏輯。 此伺服器頒發的許可證中的使用規則通過與打包時的內容相關聯的策略進行控制。
* **自定義伺服器實施**  — 您還可以使用SDK實現自己的許可伺服器。 本章中的資訊介紹了用於實現許可證伺服器的API。
