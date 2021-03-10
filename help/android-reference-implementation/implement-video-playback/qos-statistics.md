---
description: 您可以設定您的播放器，視需要從QoSProvider讀取播放和裝置統計資料。
title: 顯示QoS播放和裝置統計資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# 顯示QoS回放和設備統計資訊{#display-qos-playback-and-device-statistics}

您可以設定您的播放器，視需要從QoSProvider讀取播放和裝置統計資料。

`QoSProvider`類別提供各種統計資料，包括影格速率、描述檔位元速率、緩衝的總花費時間、緩衝嘗試次數、從第一視訊片段取得第一個位元組所花的時間、轉換第一個影格所花的時間、目前緩衝的長度和緩衝時間。

參考實作提供`QoSManager`類別，您可在其中啟用QoS覆蓋的顯示。 您也可以在「設定」使用者介面中啟用QoS可見性：

![](assets/qos-configuration.jpg)

`QoSManager`通過獲取設備資訊、連接到媒體播放器並使用最新的QoS資訊更新來跟蹤QoS統計資訊。

**啟用或禁用QoS統計報告**

1. 使用ManagerFactory建立QosManager或啟用QoS報告。

   * 要建立QosManager:
      * 此應用程式需要使用廣告工作流程功能

   QoSManager qosManager =新的QosManagerOn();

   * 要使用ManagerFactory啟用QoS統計資訊的顯示，請：

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>、config、mediaPlayer);

   >[!NOTE]
   >
   >將布林值變更為`false`會停用QoS報告。

2. 添加事件偵聽程式：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 建立QoS提供者，並將其附加至播放器活動內容：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >當播放器活動將被銷毀時，請務必調用[qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider())，通過將其從媒體播放器中分離來清除QOS提供器。

**相關API檔案**

* [類QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [類QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
