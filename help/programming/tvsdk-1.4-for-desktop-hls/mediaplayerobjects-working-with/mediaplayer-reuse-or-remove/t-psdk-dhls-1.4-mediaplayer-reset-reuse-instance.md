---
description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerStatus中定義的未初始化IDLE狀態。
title: 重設或重複使用MediaPlayer例項
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# 重設或重複使用MediaPlayer例項{#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

當您重設MediaPlayer例項時，它會傳回至MediaPlayerStatus中定義的未初始化IDLE狀態。

此操作在以下情況下非常有用：

* 您想要重複使用`MediaPlayer`例項，但需要載入新的`MediaResource`（視訊內容）並取代先前的例項。

   重設可讓您重複使用`MediaPlayer`例項，而不需釋放資源、重新建立`MediaPlayer`和重新分配資源。 `replaceCurrentItem`和`replaceCurrentResource`方法會自動為您執行這些步驟，而不需呼叫reset方法。

* 當`MediaPlayer`具有ERROR狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態中恢復的唯一方法。

1. 調用`reset`將`MediaPlayer`實例返回其未初始化狀態：

   ```
   function reset():void; 
   ```

1. 使用`MediaPlayer.replaceCurrentItem`或`MediaPlayer.replaceCurrentResource`載入另一個`MediaResource`。

   >[!TIP]
   >
   >要清除錯誤，請載入相同的`MediaResource`。

1. 收到狀態為`PREPARED`的`MediaPlaybackStatusChangeEvent.STATUS_CHANGED`時，開始播放。
