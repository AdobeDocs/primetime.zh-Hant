---
description: 您可以控制隱藏式字幕的可見度。 啟用可見性時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。
title: 控制隱藏式字幕可視性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 控制隱藏式字幕可視性 {#control-closed-caption-visibility}

您可以控制隱藏式字幕的可見度。 啟用可見性時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 相反地，幾秒後，TVSDK會在視訊中搜尋結束位置後顯示下一個隱藏式字幕文字。
>
>隱藏式字幕的可見度值定義於 `MediaPlayer.Visibility`.
>
>```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```
>

1. 等待 `MediaPlayer` 至少處於「已準備」狀態。 如需詳細資訊，請參閱 [等待有效的狀態](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md).

1. 若要取得隱藏式字幕的目前可見度設定，請在中使用getter方法 `MediaPlayer`，會傳回可見度值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 若要變更隱藏式字幕的可見度，請使用setter方法，傳遞可視度值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
