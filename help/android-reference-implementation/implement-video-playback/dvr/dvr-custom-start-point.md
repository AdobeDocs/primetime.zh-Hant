---
description: 您可以選擇自訂起始點，選擇何時輸入DVR串流，而非使用ConfigProvider類別在開始時輸入DVR串流的預設行為。
title: 選擇DVR的自訂起點
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# 選擇DVR的自訂起始點{#choosing-a-custom-starting-point-for-dvr}

您可以選擇自訂起始點，選擇何時輸入DVR串流，而非使用ConfigProvider類別在開始時輸入DVR串流的預設行為。

要通過[ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html)類設定啟動時間：

1. 啟用[isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在[retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())中設定開始時間。
1. 檢查自訂開始位置是否已啟用。
