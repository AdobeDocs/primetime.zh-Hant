---
description: 您可以控制隱藏字幕的可見性。 當可見性開啟時，將顯示當前選定的軌道。
title: 控制隱藏字幕可見性
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制隱藏字幕可見性{#control-closed-caption-visibility}

您可以控制隱藏字幕的可見性。 當可見性開啟時，將顯示當前選定的軌道。

>[!TIP]
>
>如果更改當前軌道，則可見性設定保持不變。

如果在播放器進入查找模式時顯示隱藏的字幕文本，則在查找完成後，該文本將不再顯示。 相反，在幾秒鐘後，瀏覽器TVSDK在結束查找位置後在視頻中顯示下一個隱藏的標題文本。

>[!TIP]
>
>使用 `MediaPlayer.VISIBLE` 和 `MediaPlayer.INVISIBLE`。

1. 使用 `MediaPlayer.ccVisibility` 屬性，以訪問隱藏字幕的當前可見性設定。
