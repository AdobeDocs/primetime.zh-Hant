---
description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-title: 控制隱藏字幕的可見度
title: 控制隱藏字幕的可見度
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 概觀 {#control-closed-caption-visibility}

您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。

>[!TIP]
>
>如果當播放器進入搜尋模式時顯示隱藏字幕文字，則搜尋完成後不會再顯示文字。 相反地，在數秒後，TVSDK會在結束搜尋位置後，在視訊中顯示下一個隱藏字幕文字。

>[!NOTE]
>
>隱藏字幕的可見度值在中定義 `MediaPlayer.Visibility`。>
>
```java>
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. 等待MediaPlayer至少擁有PREPARED狀態(請 [參閱等待有效狀態](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md))。
1. 若要取得隱藏字幕的目前可見性設定，請使用MediaPlayer中的getter方法，此方法會傳回可見性值。

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 若要變更隱藏字幕的可見度，請使用setter方法，從中傳遞可見度值 `MediaPlayer.Visibility`。

   例如：

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

