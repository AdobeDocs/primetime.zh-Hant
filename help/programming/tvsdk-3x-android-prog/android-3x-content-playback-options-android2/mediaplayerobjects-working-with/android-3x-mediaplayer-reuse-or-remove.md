---
description: 您可以重置、重用或釋放不再需要的MediaPlayer實例。
title: 重用或刪除MediaPlayer實例
exl-id: 8b84c7f1-713a-46b4-8eb7-d699a79e74b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 重用或刪除MediaPlayer實例 {#reuse-or-remove-a-mediaplayer-instance}

您可以重置、重用或釋放不再需要的MediaPlayer實例。

## 重置或重用MediaPlayer實例 {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

重置 `MediaPlayer` 實例，它返回到其未初始化的IDLE狀態，如中定義 `MediaPlayerStatus`。

此操作在以下情況下非常有用：

* 要重用 `MediaPlayer` 但需要載入新實例 `MediaResource` （視頻內容），並替換上一個實例。

   重置允許重用 `MediaPlayer` 實例，而不需要釋放資源並重新建立 `MediaPlayer`，並重新分配資源。

* 當 `MediaPlayer` 處於錯誤狀態，需要清除。

   >[!IMPORTANT]
   >
   >這是從ERROR狀態恢復的唯一方法。

   1. 呼叫 `reset` 返回 `MediaPlayer` 實例到其未初始化狀態：

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. 使用 `MediaPlayer.replaceCurrentResource()` 載入 `MediaResource`。

      >[!NOTE]
      >
      >要清除錯誤，請載入相同的 `MediaResource`。

   1. 當您收到 `STATUS_CHANGED` 事件回調 `PREPARED` 狀態，開始播放。

## 釋放MediaPlayer實例和資源 {#section_13A0914AFF784943ABC343F7EB249C4E}

你應該釋放 `MediaPlayer` 實例和資源，而您不再需要 `MediaResource`。

當您釋放 `MediaPlayer` 對象，與此關聯的基礎硬體資源 `MediaPlayer` 對象被取消分配。

以下是發佈 `MediaPlayer`:

* 保留不必要的資源會影響效能。
* 留下不必要的 `MediaPlayer` 對象實例化可導致移動設備的電池消耗持續。
* 如果一台設備上不支援同一視頻編解碼器的多個實例，則其他應用程式可能會出現回放失敗。

* 釋放 `MediaPlayer`。

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >在 `MediaPlayer` 實例已發佈，您不能再使用它。 如果 `MediaPlayer` 介面在發佈後調用， `MediaPlayerException` 。
