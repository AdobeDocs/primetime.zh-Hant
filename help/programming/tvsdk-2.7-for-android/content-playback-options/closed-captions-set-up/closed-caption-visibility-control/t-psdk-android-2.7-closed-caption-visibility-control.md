---
description: 您可以控制隱藏字幕的可見性。 啟用可視性後，將顯示當前選定的跟蹤。 如果更改當前軌道，則可見性設定保持不變。
title: 控制隱藏字幕可見性
exl-id: 358e32d8-7a3b-42bd-900b-dafe8eae3edf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 概述 {#control-closed-caption-visibility-overview}

您可以控制隱藏字幕的可見性。 啟用可視性後，將顯示當前選定的跟蹤。 如果更改當前軌道，則可見性設定保持不變。

>[!TIP]
>
>如果在播放器進入查找模式時顯示隱藏的字幕文本，則在查找完成後不再顯示該文本。 相反，在幾秒鐘後，TVSDK在結束查找位置後在視頻中顯示下一個隱藏字幕文本。
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

1. 等待 `MediaPlayer` 至少處於「已準備」狀態。

   有關詳細資訊，請參見ui-state-prepared-wait-for。
1. 要獲取隱藏字幕的當前可見性設定，請使用中的getter方法 `MediaPlayer`，返回可見性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 要更改隱藏字幕的可見性，請使用setter方法，通過 `MediaPlayer.Visibility`。

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
