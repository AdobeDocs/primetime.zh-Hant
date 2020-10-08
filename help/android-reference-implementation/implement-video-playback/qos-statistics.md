---
description: 您可以設定您的播放器，視需要從QoSProvider讀取播放和裝置統計資料。
seo-description: 您可以設定您的播放器，視需要從QoSProvider讀取播放和裝置統計資料。
seo-title: 顯示QoS播放和裝置統計資料
title: 顯示QoS播放和裝置統計資料
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 顯示QoS播放和裝置統計資料 {#display-qos-playback-and-device-statistics}

您可以設定您的播放器，視需要從QoSProvider讀取播放和裝置統計資料。

該類 `QoSProvider` 提供了各種統計資訊，包括幀速率、配置檔案位速率、緩衝所花費的總時間、緩衝嘗試次數、從第一個視頻片段獲取第一個位元組所花的時間、轉換第一個幀所花的時間、當前緩衝長度和緩衝時間。

參考實作提供 `QoSManager` 可啟用QoS覆蓋顯示的類別。 您也可以在「設定」使用者介面中啟用QoS可見性：

![](assets/qos-configuration.jpg)

通 `QoSManager` 過獲取設備資訊、附加到媒體播放器並使用最新的QoS資訊更新來跟蹤QoS統計。

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
   >變更布林值以停 `false` 用QoS報告。

2. 添加事件偵聽程式：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 建立QoS提供者，並將其附加至播放器活動內容：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >當播放器活動將被破壞時，請務必呼叫 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) ，將其從媒體播放器中分離，以清除QOS提供器。

**相關API檔案**

* [類QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [類QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
