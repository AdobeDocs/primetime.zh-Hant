---
description: ConfigProvider類別取得媒體播放器的設定。 您必須實作組態介面，讓功能管理員可以讀取組態資訊。
title: ConfigProvider
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

ConfigProvider類別取得媒體播放器的設定。 您必須實作組態介面，讓功能管理員可以讀取組態資訊。

您使用 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 要實作的類別 `ICCConfig`， `IAAConfig`， `IPlaybackConfig`， `IAdConfig`、和 `IQosConfig` 組態介面，讓功能管理員可以讀取組態。 例如， `ICCConfig` 是的介面 `CCManager` 設定。 組態檔會從JSON組態檔接收組態引數。

此 `ConfigProvider.java` file是Adobe實作設定介面的範例。 它會讀取以下專案的設定： `SharedPreferences`：儲存設定的位置。 您可以透過適用於貴組織的任何方式來儲存設定。 設定實作提供設定來源的包裝函式。
