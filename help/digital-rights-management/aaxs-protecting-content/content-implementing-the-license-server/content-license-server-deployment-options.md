---
title: 授權伺服器部署選項
description: 授權伺服器部署選項
copied-description: true
exl-id: c7422a8f-2cd1-4ace-8706-eb3e5a55eac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 授權伺服器部署選項{#license-server-deployment-options}

可使用下列其中一個選項來部署License Server：

* **適用於受保護串流的Adobe Access Server**  — 此License Server已針對串流最佳化。 例如，您可以設定伺服器以使用「Adobe存取」進行AdobeHTTP Dynamic Streaming。 此伺服器部署簡單，只需很少的設定，可支援多個租使用者，並可達到高水準的擴充性。 不過，由於此實作已針對串流最佳化，因此不支援完整的Adobe存取功能。 例如，不支援使用者名稱/密碼驗證、網域和授權鏈結。 此伺服器所核發的授權中的使用規則，是由伺服器設定檔所控制，該設定檔會覆寫封裝時所使用的原則。 請參閱 *適用於受保護串流的Adobe Access Server指南* 此伺服器支援之使用規則的詳細資訊。
* **參考實作授權伺服器**  — 使用此設定作為自訂伺服器實作的起點。 這是授權伺服器實作的範例，包括原始程式碼，示範如何使用Adobe存取SDK中的API處理所有型別的請求，以及如何實作資料庫支援的自訂商業邏輯。 此伺服器所核發的授權中的使用規則，是由封裝時與內容相關的原則所控制。
* **自訂伺服器實作**  — 您也可以使用SDK實作自己的授權伺服器。 本章中的資訊說明用於實作授權伺服器的API。
