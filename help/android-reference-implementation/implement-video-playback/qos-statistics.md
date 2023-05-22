---
description: 您可以設定播放器，以便根據需要從QoSProvider中讀取播放和設備統計資訊。
title: 顯示QoS回放和設備統計資訊
exl-id: 369b6e9a-70a2-4f62-a1bf-f69030c5d6c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 顯示QoS回放和設備統計資訊 {#display-qos-playback-and-device-statistics}

您可以設定播放器，以便根據需要從QoSProvider中讀取播放和設備統計資訊。

的 `QoSProvider` 類提供各種統計資訊，包括幀速率、配置檔案比特率、緩衝所花費的總時間、緩衝嘗試次數、從第一視頻片段獲取第一個位元組所花的時間、呈現第一幀所花的時間、當前緩衝的長度和緩衝時間。

參考實現提供 `QoSManager` 類，您可以在其中啟用QoS覆蓋的顯示。 還可以在「設定」用戶介面中啟用QoS可見性：

![](assets/qos-configuration.jpg)

的 `QoSManager` 通過獲取設備資訊、連接到媒體播放器以及使用最新QoS資訊更新來跟蹤QoS統計。

**啟用或禁用QoS統計報告**

1. 使用ManagerFactory建立QosManager或啟用QoS報告。

   * 要建立QosManager:
      * 此應用程式需要使用廣告工作流功能

   QoSManager qosManager =新的QosManagerOn();

   * 要使用ManagerFactory啟用QoS統計資訊的顯示，請執行以下操作：

   qosManager = ManagerFactory.getQosManager(
   <b>真</b>, config, mediaPlayer);

   >[!NOTE]
   >
   >將布爾值更改為 `false` 禁用QoS報告。

2. 添加事件偵聽器：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 建立QoS提供程式並將其附加到播放器活動上下文：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >當玩家活動將被破壞時，請確保 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) 通過將QOS提供程式從媒體播放器中分離來清除它。

**相關API文檔**

* [類QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [類QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManager事件監聽器](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QoItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
