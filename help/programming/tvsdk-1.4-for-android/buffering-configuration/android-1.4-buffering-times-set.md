---
description: 為了提供更流暢的觀看體驗，TVSDK有時會緩衝視頻流。 您可以配置播放器緩衝區的方式。
title: 設定緩衝時間
exl-id: 4542d10a-b6f8-430d-8b9a-5a358d1c0e9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 緩衝 {#buffering}

為了提供更流暢的觀看體驗，TVSDK有時會緩衝視頻流。 您可以配置播放器緩衝區的方式。

TVSDK定義至少30秒的回放緩衝長度，以及在媒體開始播放之前至少2秒的初始緩衝時間。 應用程式調用後 `play` 但是在播放開始之前，TVSDK會將媒體緩衝到初始時間，以便在真正開始播放時提供平穩的開始。

可以通過定義新的緩衝策略來更改緩衝時間，並且可以通過使用即時開啟來更改初始緩衝的時間。

## 設定緩衝時間 {#set-buffering-times}

的 `MediaPlayer` 提供了設定和獲取初始緩衝時間和回放緩衝時間的方法。

>[!TIP]
>
>如果在開始播放之前未設定緩衝區控制參數，則初始緩衝區的媒體播放器預設為2秒，當前播放緩衝區的時間預設為30秒。

1. 設定 `BufferControlParameters` 對象，它封裝了初始緩衝時間和回放緩衝時間控制參數：

       此類提供兩種工廠方法：
   
   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```java
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```

   * 要設定初始緩衝時間和播放緩衝時間，請執行以下操作：

      ```java
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

      這些方法 `IllegalArgumentException` 如果參數無效，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 要設定緩衝區參數值，請使用 `MediaPlayer` 方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要獲取當前緩衝區參數值，請使用 `MediaPlayer` 方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   如果AVE無法設定指定的值，媒體播放器將 `ERROR` 狀態為錯誤代碼 `SET_BUFFER_PARAMETERS_ERROR`。

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，要將初始緩衝區設定為2秒，將回放緩衝區時間設定為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

黃金時段參考實現演示了該功能；使用應用程式的設定設定緩衝區值。
