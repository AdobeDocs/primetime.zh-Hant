---
description: 您可以選擇何時輸入DVR流的自定義起始點，而不是使用ConfigProvider類在開始時輸入DVR流的預設行為。
title: 為DVR選擇自定義起點
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 為DVR選擇自定義起點 {#choosing-a-custom-starting-point-for-dvr}

您可以選擇何時輸入DVR流的自定義起始點，而不是使用ConfigProvider類在開始時輸入DVR流的預設行為。

在 [配置提供程式](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) 類：

1. 啟用 [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled())。
1. 在中設定開始時間 [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref())。
1. 檢查自定義起始位置是否已啟用。
