---
description: ConfigProvider類獲取媒體播放器的配置。 必須實現配置介面，以便功能管理器可以讀取配置資訊。
title: 配置提供程式
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 配置提供程式 {#configprovider}

ConfigProvider類獲取媒體播放器的配置。 必須實現配置介面，以便功能管理器可以讀取配置資訊。

使用 [配置提供程式](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 類以實現 `ICCConfig`。 `IAAConfig`。 `IPlaybackConfig`。 `IAdConfig`, `IQosConfig` 配置介面，以便功能管理器能夠讀取配置。 例如， `ICCConfig` 是 `CCManager` 配置。 配置檔案從JSON配置檔案接收配置參數。

的 `ConfigProvider.java` file是Adobe實現配置介面的示例。 它從 `SharedPreferences`，其中儲存了配置。 您可以以任何適合您組織的方式儲存您的配置。 配置實現為配置源提供包裝。
