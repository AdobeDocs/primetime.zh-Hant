---
seo-title: 全域伺服器組態資料
title: 全域伺服器組態資料
uuid: a1557b3e-9a08-4623-a62d-8ebc308eae15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 全局伺服器配置資料{#global-server-configuration-data}

除了許可證伺服器使用的配置外，`HandlerConfiguration`還儲存可發送到客戶機的配置資訊，以控制許可證的執行方式。 這是通過建立`ServerConfigData`類並調用`HandlerConfiguration.setServerConfigData()`來完成的。 這些設定僅適用於此授權伺服器所核發的授權。

時鐘回退容限是授權伺服器可設定的屬性之一，以控制用戶端執行授權的方式。 依預設，使用者可將其電腦時鐘設定在4小時前，而不會使授權失效。 如果授權伺服器運算子想要使用不同的設定，則可在`ServerConfigData`類別中設定新值。 當您變更其中任何設定的值時，請務必呼叫`setVersion()`以增加版本號碼。 新值僅在客戶端上的版本早於當前`ServerConfigData`版本時才會發送到客戶端。
