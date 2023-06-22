---
title: 全域伺服器設定資料
description: 全域伺服器設定資料
copied-description: true
exl-id: 0afce045-1dd7-4fe7-84b7-d60068b3423a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# 全域伺服器設定資料{#global-server-configuration-data}

除了授權伺服器使用的設定， `HandlerConfiguration` 儲存可傳送給使用者端的設定資訊，以控制如何強制執行授權。 這是透過建立 `ServerConfigData` 類別和呼叫 `HandlerConfiguration.setServerConfigData()` （這些設定只適用於此授權伺服器發行的授權）。 時鐘回溯容許度是授權伺服器可以設定的一個屬性，用來控制使用者端執行授權的方式。 依預設，使用者可將電腦時鐘設定回4小時，而不會讓授權失效。 如果授權伺服器操作員想要使用不同的設定，則可以在以下位置設定新值： `ServerConfigData` 類別。 當您變更其中任何設定的值時，請務必透過呼叫來增加版本號碼 `setVersion()`. 只有在使用者端上的版本低於目前版本時，才會將新值傳送給使用者端 `ServerConfigData` 版本。
