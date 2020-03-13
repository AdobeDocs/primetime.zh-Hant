---
description: 為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器緩衝的方式。
seo-description: 為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器緩衝的方式。
seo-title: 設定緩衝時間
title: 設定緩衝時間
uuid: 5a3945a4-1935-4797-b19d-84989850a487
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 緩衝 {#buffering}

為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器緩衝的方式。

TVSDK定義至少30秒的播放緩衝長度，以及媒體開始播放之前至少2秒的初始緩衝時間。 在應用程式呼 `play` 叫後，但在播放開始前，TVSDK會將媒體緩衝至初始時間，以在實際開始播放時提供順暢的開始。

通過定義新的緩衝策略，可以更改緩衝時間；通過使用即時啟動，可以更改初始緩衝何時發生。

## 設定緩衝時間 {#set-buffering-times}

提供 `MediaPlayer` 了設定和獲取初始緩衝時間和回放緩衝時間的方法。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝區控制參數，媒體播放器預設初始緩衝區為2秒，而持續播放緩衝區時間為30秒。

1. 設定對象， `BufferControlParameters` 封裝初始緩衝時間和回放緩衝時間控制參數：

       此類提供兩種工廠方法：
   
   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * 要同時設定初始和播放緩衝時間：

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      這些方法會在 `IllegalArgumentException` 參數無效時拋出，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 要設定緩衝區參數值，請使用以下 `MediaPlayer` 方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要獲取當前緩衝區參數值，請使用以下 `MediaPlayer` 方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   如果AVE無法設定指定的值，媒體播放器會以錯 `ERROR` 誤碼進入狀態 `SET_BUFFER_PARAMETERS_ERROR`。

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，若要將初始緩衝區設為2秒，而播放緩衝時間設為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime參考實作會示範此功能；使用應用程式的設定來設定緩衝值。