---
description: 當您不再需要MediaResource時，應該發行MediaPlayer例項和資源。
title: 發行MediaPlayer例項和資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 發行MediaPlayer例項和資源{#release-a-mediaplayer-instance-and-resources}

當您不再需要MediaResource時，應該發行MediaPlayer例項和資源。

當您發行 `MediaPlayer` 物件，與此物件關聯的基本硬體資源 `MediaPlayer` 物件會取消配置。

以下是發行「 」的一些理由 `MediaPlayer`：

* 保留不必要的資源可能會影響效能。
* 如果裝置不支援相同視訊轉碼器的多個執行個體，其他應用程式可能會發生播放失敗。

1. 發行 `MediaPlayer`.

   ```
   function release():void;
   ```

在 `MediaPlayer` 例項已發行，您無法再使用。 若有任何方法屬於 `MediaPlayer` 介面在發行後呼叫，透過 `IllegalStateException` 擲回。
