---
description: 您可以控制隱藏字幕的可見度。 啟用可見性後，會顯示目前選取的追蹤。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-description: 您可以控制隱藏字幕的可見度。 啟用可見性後，會顯示目前選取的追蹤。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-title: 控制隱藏字幕的可見度
title: 控制隱藏字幕的可見度
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 控制隱藏字幕的可見度 {#control-closed-caption-visibility}

您可以控制隱藏字幕的可見度。 啟用可見性後，會顯示目前選取的追蹤。 如果您變更了目前的軌道，可見度設定會維持不變。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏字幕文字，則在搜尋完成後不會再顯示文字。 相反地，在數秒後，TVSDK會在結束搜尋位置後，在視訊中顯示下一個隱藏字幕文字。
>
>隱藏字幕的可見度值在中定義 `MediaPlayer.Visibility`。
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等待至 `MediaPlayer` 少處於PREPARED狀態。 如需詳細資訊，請 [參閱等待有效狀態](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)。

1. 若要取得隱藏字幕的目前可見度設定，請使用中的getter方 `MediaPlayer`法，其會傳回可見度值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 若要變更隱藏字幕的可見度，請使用setter方法，從中傳遞可見度值 `MediaPlayer.Visibility`。

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
