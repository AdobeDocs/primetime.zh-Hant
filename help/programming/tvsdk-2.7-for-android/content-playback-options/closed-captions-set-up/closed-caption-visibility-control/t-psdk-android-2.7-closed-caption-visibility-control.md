---
description: 您可以控制隱藏式字幕的可見度。 啟用可見性後，會顯示目前選取的曲目。 如果變更目前哪個軌跡，可視性設定會維持不變。
title: 控制隱藏式字幕可見度
exl-id: 358e32d8-7a3b-42bd-900b-dafe8eae3edf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 概觀 {#control-closed-caption-visibility-overview}

您可以控制隱藏式字幕的可見度。 啟用可見性後，會顯示目前選取的曲目。 如果變更目前哪個軌跡，可視性設定會維持不變。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 相反地，幾秒後，TVSDK會在視訊中顯示搜尋結束位置後的下一個隱藏式字幕文字。
>
>隱藏式字幕的可見度值定義於 `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等候 `MediaPlayer` 至少處於「已準備」狀態。

   如需詳細資訊，請參閱ui-state-prepared-wait-for 。
1. 若要取得隱藏式字幕的目前可見度設定，請在中使用getter方法 `MediaPlayer`，會傳回可見度值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 若要變更隱藏式字幕的可見度，請使用setter方法，傳遞可視度值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
