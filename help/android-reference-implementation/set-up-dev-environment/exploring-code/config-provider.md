---
description: ConfigProvider類別會取得媒體播放器的設定。 您必須實作設定介面，讓功能管理員可以讀取設定資訊。
seo-description: ConfigProvider類別會取得媒體播放器的設定。 您必須實作設定介面，讓功能管理員可以讀取設定資訊。
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

ConfigProvider類別會取得媒體播放器的設定。 您必須實作設定介面，讓功能管理員可以讀取設定資訊。

使用[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)類別來實作`ICCConfig`、`IAAConfig`、`IPlaybackConfig`、`IAdConfig`和`IQosConfig`組態介面，讓功能管理員可以讀取組態。 例如，`ICCConfig`是`CCManager`配置的介面。 設定檔案會從JSON設定檔案接收設定參數。

`ConfigProvider.java`檔案是Adobe實作組態介面的範例。 它會從`SharedPreferences`讀取設定，儲存設定。 您可以以任何適合您組織的方式儲存您的設定。 config實現為配置源提供了包裝函式。