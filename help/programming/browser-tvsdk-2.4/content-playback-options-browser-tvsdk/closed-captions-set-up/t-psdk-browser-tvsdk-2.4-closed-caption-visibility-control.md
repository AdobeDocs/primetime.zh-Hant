---
description: 您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。
title: 控制隱藏式字幕可視性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制隱藏式字幕可視性{#control-closed-caption-visibility}

您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。

>[!TIP]
>
>如果變更目前哪個軌跡，可視性設定會保持相同。

如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 相反地，幾秒後，瀏覽器TVSDK會在視訊中搜尋結束位置後顯示下一個隱藏式字幕文字。

>[!TIP]
>
>隱藏式字幕的可見度值是由下列專案所控制 `MediaPlayer.VISIBLE` 和 `MediaPlayer.INVISIBLE`.

1. 使用 `MediaPlayer.ccVisibility` 屬性來存取隱藏式字幕的目前可見度設定。
