---
description: 您可以視需要經常將播放器設定為從QoSProvider讀取播放和裝置統計資料。
title: 顯示QoS播放和裝置統計資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 顯示QoS播放和裝置統計資料 {#display-qos-playback-and-device-statistics}

您可以視需要經常將播放器設定為從QoSProvider讀取播放和裝置統計資料。

此 `QoSProvider` class提供各種統計資料，包括影格速率、設定檔位元速率、緩衝花費的總時間、緩衝嘗試次數、從第一個視訊片段取得第一個位元組所花的時間、轉譯第一個影格所花的時間、目前緩衝的長度，以及緩衝時間。

參考實作提供 `QoSManager` 可啟用顯示QoS覆蓋的類別。 您也可以在「設定」使用者介面中啟用QoS可見性：

![](assets/qos-configuration.jpg)

此 `QoSManager` 透過取得裝置資訊、附加至媒體播放器並使用最新的QoS資訊更新來追蹤QoS統計資料。

**啟用或停用QoS統計報表**

1. 使用ManagerFactory建立QosManager或啟用QoS報告。

   * 若要建立QosManager：
      * 此應用程式需要使用廣告工作流程功能

   QoSManager qosManager =新QosManagerOn()；

   * 若要使用ManagerFactory來啟用QoS統計資料的顯示：

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>，設定， mediaPlayer)；

   >[!NOTE]
   >
   >將布林值變更為 `false` 停用QoS報告。

2. 新增事件接聽程式：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 建立QoS提供者，並將其附加至播放器活動內容：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >當播放器活動即將損毀，請務必呼叫 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) 將QOS提供者從媒體播放器中斷連結，以清理它。

**相關API檔案**

* [類別QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [類別QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [Qos專案](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
