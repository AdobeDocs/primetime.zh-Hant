---
description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。
seo-description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。
seo-title: 控制隱藏字幕的可見度
title: 控制隱藏字幕的可見度
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 控制隱藏字幕可見度{#control-closed-caption-visibility}

您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。

>[!TIP]
>
>如果您變更了目前的軌道，可見度設定會維持不變。

如果當播放器進入搜尋模式時顯示隱藏字幕文字，則在搜尋完成後不會再顯示文字。 反之，在數秒後，瀏覽器TVSDK會在結束搜尋位置後，在視訊中顯示下一個隱藏字幕文字。

>[!TIP]
>
>隱藏字幕的可見度值由`MediaPlayer.VISIBLE`和`MediaPlayer.INVISIBLE`控制。

1. 使用`MediaPlayer.ccVisibility`屬性來存取隱藏字幕的目前可見性設定。

