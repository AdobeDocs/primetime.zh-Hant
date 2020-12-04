---
description: 您可以選擇自訂起始點，以選擇何時輸入DVR串流，而非使用ConfigProvider類別在開始時輸入DVR串流的預設行為。
seo-description: 您可以選擇自訂起始點，以選擇何時輸入DVR串流，而非使用ConfigProvider類別在開始時輸入DVR串流的預設行為。
seo-title: 選擇DVR的自訂起點
title: 選擇DVR的自訂起點
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# 選擇DVR的自訂起始點{#choosing-a-custom-starting-point-for-dvr}

您可以選擇自訂起始點，以選擇何時輸入DVR串流，而非使用ConfigProvider類別在開始時輸入DVR串流的預設行為。

要通過[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)類設定啟動時間：

1. 啟用[isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在[retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())中設定開始時間。
1. 檢查自訂開始位置是否已啟用。
