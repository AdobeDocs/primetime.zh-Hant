---
description: 當您不再需要MediaResource時，應該發行MediaPlayer實例和資源。
seo-description: 當您不再需要MediaResource時，應該發行MediaPlayer實例和資源。
seo-title: 發行MediaPlayer實例和資源
title: 發行MediaPlayer實例和資源
uuid: e7b2112e-8add-4789-9345-5f829d39d639
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 發行MediaPlayer實例和資源{#release-a-mediaplayer-instance-and-resources}

當您不再需要MediaResource時，應該發行MediaPlayer實例和資源。

釋放`MediaPlayer`對象時，將取消分配與此`MediaPlayer`對象關聯的基礎硬體資源。

以下是發佈`MediaPlayer`的一些理由：

* 保留不必要的資源可能會影響效能。
* 如果裝置不支援同一視訊codec的多個執行個體，其他應用程式可能會發生播放失敗。

1. 釋放`MediaPlayer`。

   ```
   function release():void;
   ```

在`MediaPlayer`實例發佈後，您無法再使用它。 如果在`MediaPlayer`介面發佈後調用了任何方法，則會拋出`IllegalStateException`。