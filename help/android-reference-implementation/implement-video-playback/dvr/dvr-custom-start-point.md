---
description: 您可以選擇自訂的起始點，作為何時輸入DVR資料流的起點，而不是使用ConfigProvider類別從頭輸入DVR資料流的預設行為。
title: 選擇DVR的自訂起點
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 選擇DVR的自訂起點 {#choosing-a-custom-starting-point-for-dvr}

您可以選擇自訂的起始點，作為何時輸入DVR資料流的起點，而不是使用ConfigProvider類別從頭輸入DVR資料流的預設行為。

若要透過 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 類別：

1. 啟用 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. 設定開始時間 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 檢查自訂開始位置是否已啟用。
