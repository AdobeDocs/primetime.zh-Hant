---
description: 在不再需要MediaResource時，應釋放MediaPlayer實例和資源。
title: 釋放MediaPlayer實例和資源
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 釋放MediaPlayer實例和資源{#release-a-mediaplayer-instance-and-resources}

在不再需要MediaResource時，應釋放MediaPlayer實例和資源。

當您釋放 `MediaPlayer` 對象，與此關聯的基礎硬體資源 `MediaPlayer` 對象被取消分配。

以下是發佈 `MediaPlayer`:

* 保留不必要的資源會影響效能。
* 如果一台設備上不支援同一視頻編解碼器的多個實例，則其他應用程式可能會出現回放失敗。

1. 釋放 `MediaPlayer`。

   ```
   function release():void;
   ```

在 `MediaPlayer` 實例已發佈，您不能再使用它。 如果 `MediaPlayer` 介面在發佈後調用， `IllegalStateException` 。
