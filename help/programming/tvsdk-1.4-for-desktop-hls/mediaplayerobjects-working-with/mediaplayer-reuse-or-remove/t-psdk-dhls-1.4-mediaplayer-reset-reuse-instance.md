---
description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerStatus中定義的未初始化IDLE狀態。
seo-description: 當您重設MediaPlayer例項時，它會傳回至MediaPlayerStatus中定義的未初始化IDLE狀態。
seo-title: 重設或重複使用MediaPlayer例項
title: 重設或重複使用MediaPlayer例項
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97

---


# 重設或重複使用MediaPlayer例項{#reset-or-reuse-a-mediaplayer-instance}

您可以重設、重複使用或發行您不再需要的MediaPlayer例項。

當您重設MediaPlayer例項時，它會傳回至MediaPlayerStatus中定義的未初始化IDLE狀態。

此操作在以下情況下非常有用：

* 您想要重複使用 `MediaPlayer` 例項，但需要載入新 `MediaResource` （視訊內容）並取代先前的例項。

   重設可讓您重複使用例 `MediaPlayer` 項，而不需要釋放資源、重新建立資 `MediaPlayer`源和重新分配資源。 這些 `replaceCurrentItem` 和方 `replaceCurrentResource` 法會自動為您執行這些步驟，而不需呼叫reset方法。

* 當具有 `MediaPlayer` 錯誤狀態且需要清除時。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態中恢復的唯一方法。

1. 呼叫 `reset` 以將實 `MediaPlayer` 例返回到未初始化狀態：

   ```
   function reset():void; 
   ```

1. 使用 `MediaPlayer.replaceCurrentItem` 或 `MediaPlayer.replaceCurrentResource` 載入其他 `MediaResource`。

   >[!TIP]
   >
   >若要清除錯誤，請載入相同的錯誤 `MediaResource`。

1. 當您收到狀態 `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` 為的 `PREPARED` 時，請開始播放。
