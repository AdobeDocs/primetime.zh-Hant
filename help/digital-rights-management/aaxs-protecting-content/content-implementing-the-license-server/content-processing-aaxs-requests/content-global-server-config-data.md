---
seo-title: 全域伺服器組態資料
title: 全域伺服器組態資料
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 全域伺服器組態資料{#global-server-configuration-data}

除了授權伺服器使用的設定外，還會儲 `HandlerConfiguration` 存可傳送至用戶端的設定資訊，以控制授權的執行方式。 這是透過建立類別和呼叫 `ServerConfigData` 來完成的( `HandlerConfiguration.setServerConfigData()` 這些設定僅適用於此授權伺服器所核發的授權)。 時鐘回退容限是授權伺服器可設定的屬性之一，以控制用戶端執行授權的方式。 依預設，使用者可將其電腦時鐘設定在4小時前，而不會使授權失效。 如果授權伺服器運算子想要使用不同的設定，可以在類別中設定新 `ServerConfigData` 值。 當您變更其中任何設定的值時，請務必透過呼叫來增加版本號碼 `setVersion()`。 新值只有在用戶端上的版本低於目前版本時才會傳送至用戶 `ServerConfigData` 端。
