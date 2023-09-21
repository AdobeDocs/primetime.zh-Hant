---
description: 您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。
title: 控制隱藏式字幕可視性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 概觀 {#control-closed-caption-visibility}

您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 相反地，幾秒後，TVSDK會在視訊中搜尋結束位置後顯示下一個隱藏式字幕文字。

>[!NOTE]
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

1. 等待MediaPlayer至少具有PREPARED狀態(請參閱 [等待有效的狀態](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md))。
1. 若要取得隱藏式字幕的目前可見度設定，請使用MediaPlayer中的getter方法，此方法會傳回可見度值。

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 若要變更隱藏式字幕的可見度，請使用setter方法，傳遞可視度值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
