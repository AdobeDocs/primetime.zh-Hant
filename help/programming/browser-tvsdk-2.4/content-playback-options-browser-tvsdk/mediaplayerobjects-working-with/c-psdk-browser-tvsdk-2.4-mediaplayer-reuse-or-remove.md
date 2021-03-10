---
description: 您可以重設、重複使用或發行您不再需要的MediaPlayer例項。
title: 重複使用或移除MediaPlayer例項
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# 重複使用或移除MediaPlayer例項{#reuse-or-remove-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

## 重設或重複使用MediaPlayer例項{#section_C183E6164C184C3CBC5321FC6A2528EA}

您可以重設`MediaPlayer`實例，使其返回到`MediaPlayerStatus`中定義的未初始化的IDLE狀態。 您也可以使用先前載入的媒體資源來取代目前的媒體項目或設定新的媒體項目。

此操作在以下情況下非常有用：

* 您想要重複使用`MediaPlayer`例項，但需要載入新的`MediaResource`（視訊內容）並取代先前的例項。

   重設可讓您重複使用`MediaPlayer`例項，而不需釋放資源、重新建立`MediaPlayer`和重新分配資源。 `replaceCurrentItem`方法會自動為您執行這些步驟。

* 當`MediaPlayer`處於ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

1. 調用`MediaPlayer.reset()`將`MediaPlayer`實例返回其未初始化狀態：

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. 呼叫`MediaPlayer.replaceCurrentItem()`以載入另一個`MediaResource`

   >[!TIP]
   >
   >要清除錯誤，請載入相同的`MediaResource`。

1. 調用`prepareToPlay()`方法。

   >[!NOTE]
   >
   >當您收到`MediaPlaybackStatusChangeEvent.STATUS_CHANGED`事件且狀態為PREPARED時，可以開始播放。

## 發行MediaPlayer實例和資源{#section_2D159975C82245098E7078FE0B1578CE}

當您不再需要MediaResource時，應釋放`MediaPlayer`實例和資源。

以下是發佈`MediaPlayer`的一些理由：

* 保留不必要的資源可能會影響效能。
* 留下不必要的`MediaPlayer`物件可持續耗用行動裝置的電池。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

* 釋放`MediaPlayer`。

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >在`MediaPlayer`實例發佈後，您無法再使用它。 如果在`MediaPlayer`介面發佈後調用了任何方法，則會拋出`IllegalStateException`。

