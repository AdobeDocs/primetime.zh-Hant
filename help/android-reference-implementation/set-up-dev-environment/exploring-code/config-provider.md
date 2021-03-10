---
description: ConfigProvider類別會取得媒體播放器的設定。 您必須實作設定介面，讓功能管理員可以讀取設定資訊。
title: ConfigProvider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

ConfigProvider類別會取得媒體播放器的設定。 您必須實作設定介面，讓功能管理員可以讀取設定資訊。

使用[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)類別來實作`ICCConfig`、`IAAConfig`、`IPlaybackConfig`、`IAdConfig`和`IQosConfig`組態介面，讓功能管理員可以讀取組態。 例如，`ICCConfig`是`CCManager`配置的介面。 設定檔案會從JSON設定檔案接收設定參數。

`ConfigProvider.java`檔案是Adobe實施配置介面的示例。 它會從`SharedPreferences`讀取設定，儲存設定。 您可以以任何適合您組織的方式儲存您的設定。 config實現為配置源提供了包裝函式。