---
description: 您可以控制隱藏字幕的可見性。 當可見性開啟時，將顯示當前選定的軌道。 如果更改當前軌道，則可見性設定保持不變。
title: 控制隱藏字幕可見性
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 概述 {#control-closed-caption-visibility}

您可以控制隱藏字幕的可見性。 當可見性開啟時，將顯示當前選定的軌道。 如果更改當前軌道，則可見性設定保持不變。

>[!TIP]
>
>如果在播放器進入查找模式時顯示隱藏的字幕文本，則在查找完成後不再顯示該文本。 相反，在幾秒鐘後，TVSDK在結束查找位置後在視頻中顯示下一個隱藏字幕文本。

>[!NOTE]
>
>隱藏字幕的可見性值在中定義 `MediaPlayer.Visibility`。
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等待MediaPlayer至少具有PREPARED狀態(請參見 [等待有效狀態](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md))。
1. 要獲取隱藏字幕的當前可見性設定，請使用MediaPlayer中的getter方法，該方法返回可見性值。

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 要更改隱藏字幕的可見性，請使用setter方法，通過 `MediaPlayer.Visibility`。

   例如：

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
