---
seo-title: 授權伺服器部署選項
title: 授權伺服器部署選項
uuid: 297c587f-23e2-4bb5-911b-72d7b82370f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 授權伺服器部署選項{#license-server-deployment-options}

您可使用下列其中一個選項來部署授權伺服器：

* **Adobe Access Server for Protected Streaming** —此授權伺服器已針對串流最佳化。 例如，您可以使用Adobe Access為Adobe HTTP Dynamic Streaming設定伺服器。 此伺服器可輕鬆部署，所需的組態非常少，而且可支援多個租戶，並可實現高階的擴充性。 不過，由於此實作已針對串流最佳化，因此不支援完整的Adobe Access功能。 例如，使用者名稱／密碼驗證、網域和授權鏈結不受支援。 此伺服器所核發之授權中的使用規則會透過伺服器組態檔加以控制，而此組態檔會覆寫封裝時使用的原則。 如需 *此伺服器支援之使用規則的詳細資訊，請參閱Adobe Access Server for Protected Streaming Guide* 。
* **參考實作授權伺服器** —使用此設定作為自訂伺服器實作的起點。 這是授權伺服器實作的範例，包括原始碼，可示範如何使用Adobe Access SDK中的API來處理所有類型的請求，以及如何實作由資料庫支援的自訂商業邏輯。 此伺服器所核發之授權中的使用規則，是透過封裝時與內容相關的原則加以控制。
* **自訂伺服器實作** —您也可以使用SDK實作您自己的授權伺服器。 本章中的資訊說明用於實作授權伺服器的API。

