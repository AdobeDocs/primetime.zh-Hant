---
description: 您可以選擇自訂的起始點來決定何時輸入DVR資料流，而不是預設行為，即一開始使用ConfigProvider類別輸入DVR資料流。
title: 選擇DVR的自訂起點
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 選擇DVR的自訂起點 {#choosing-a-custom-starting-point-for-dvr}

您可以選擇自訂的起始點來決定何時輸入DVR資料流，而不是預設行為，即一開始使用ConfigProvider類別輸入DVR資料流。

若要透過設定開始時間 [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 類別：

1. 啟用 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. 設定開始時間於 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. 檢查自訂開始位置是否已啟用。
