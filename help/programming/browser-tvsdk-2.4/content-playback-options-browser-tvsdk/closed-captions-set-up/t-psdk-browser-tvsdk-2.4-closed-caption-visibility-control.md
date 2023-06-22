---
description: 您可以控制隱藏式字幕的可見度。 當可見性開啟時，會顯示目前選取的軌跡。
title: 控制隱藏式字幕可見度
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制隱藏式字幕可見度{#control-closed-caption-visibility}

您可以控制隱藏式字幕的可見度。 當可見性開啟時，會顯示目前選取的軌跡。

>[!TIP]
>
>如果變更目前哪個軌跡，可視性設定會維持不變。

如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 而是在幾秒後，瀏覽器TVSDK會在搜尋結束位置後，在視訊中顯示下一個隱藏式字幕文字。

>[!TIP]
>
>隱藏式字幕的可見度值由控制 `MediaPlayer.VISIBLE` 和 `MediaPlayer.INVISIBLE`.

1. 使用 `MediaPlayer.ccVisibility` 屬性以存取隱藏式字幕的目前可見度設定。
