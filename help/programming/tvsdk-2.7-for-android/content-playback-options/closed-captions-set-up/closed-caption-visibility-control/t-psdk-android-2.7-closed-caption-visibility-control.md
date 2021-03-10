---
description: 您可以控制隱藏字幕的可見度。 啟用可見性後，會顯示目前選取的追蹤。 如果您變更了目前的軌道，可見度設定會維持不變。
title: 控制隱藏字幕的可見度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---


# 概述{#control-closed-caption-visibility-overview}

您可以控制隱藏字幕的可見度。 啟用可見性後，會顯示目前選取的追蹤。 如果您變更了目前的軌道，可見度設定會維持不變。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏字幕文字，則在搜尋完成後不會再顯示文字。 相反地，在數秒後，TVSDK會在結束搜尋位置後，在視訊中顯示下一個隱藏字幕文字。
>
>隱藏字幕的可見度值定義在`MediaPlayer.Visibility`中。
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等待`MediaPlayer`至少處於「已準備」狀態。

   如需詳細資訊，請參閱ui-state-prepared-wait-for。
1. 若要取得隱藏字幕的目前可見性設定，請使用`MediaPlayer`中的getter方法，此方法會傳回可見性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 若要變更隱藏字幕的可見度，請使用setter方法，從`MediaPlayer.Visibility`傳遞可見度值。

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

