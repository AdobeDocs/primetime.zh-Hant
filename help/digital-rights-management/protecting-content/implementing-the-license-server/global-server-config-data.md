---
title: 全局伺服器配置資料
description: 全局伺服器配置資料
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 全局伺服器配置資料{#global-server-configuration-data}

除了許可證伺服器使用的配置外， `HandlerConfiguration` 儲存可發送到客戶端的配置資訊，以控制如何強制實施許可證。 通過建立 `ServerConfigData` 類和呼叫 `HandlerConfiguration.setServerConfigData()`。 這些設定僅適用於此許可證伺服器頒發的許可證。

時鐘向後容錯是許可證伺服器可以設定的一個屬性，以控制客戶端如何實施許可證。 預設情況下，用戶可以將其電腦時鐘設定回4小時，而不會使許可證失效。 如果許可證伺服器操作員希望使用其他設定，可以在 `ServerConfigData` 類。 更改這些設定中的任何一個的值時，請確保通過調用來增加版本號 `setVersion()`。 僅當客戶端上的版本比當前版本舊時，新值才會發送到客戶端 `ServerConfigData` 。
