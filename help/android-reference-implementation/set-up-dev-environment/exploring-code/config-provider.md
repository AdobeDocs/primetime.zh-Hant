---
description: ConfigProvider類別會取得媒體播放器的設定。 您必須實作組態介面，讓功能管理員可以讀取組態資訊。
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

ConfigProvider類別會取得媒體播放器的設定。 您必須實作組態介面，讓功能管理員可以讀取組態資訊。

您使用 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 要實作「 」的類別 `ICCConfig`， `IAAConfig`， `IPlaybackConfig`， `IAdConfig`、和 `IQosConfig` 組態介面，讓功能管理員可以讀取組態。 例如， `ICCConfig` 是的介面 `CCManager` 設定。 組態檔會從JSON組態檔接收組態引數。

此 `ConfigProvider.java` file是Adobe實作設定介面的範例。 它會讀取以下專案的設定： `SharedPreferences`，會儲存設定。 您可以透過適用於貴組織的任何方式來儲存設定。 設定實作提供設定來源的包裝函式。
