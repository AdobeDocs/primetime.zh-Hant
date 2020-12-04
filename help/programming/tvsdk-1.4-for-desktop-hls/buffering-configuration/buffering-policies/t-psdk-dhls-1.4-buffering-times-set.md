---
description: MediaPlayer提供設定和取得初始緩衝時間和播放緩衝時間的方法。
seo-description: MediaPlayer提供設定和取得初始緩衝時間和播放緩衝時間的方法。
seo-title: 設定緩衝時間
title: 設定緩衝時間
uuid: 25142b01-5381-49c9-b89a-24c858faaf13
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 設定緩衝時間{#set-buffering-times}

MediaPlayer提供設定和取得初始緩衝時間和播放緩衝時間的方法。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝區控制參數，媒體播放器預設初始緩衝區為2秒，而持續播放緩衝區時間為30秒。

1. 設定`BufferControlParameters`對象，該對象封裝初始緩衝時間和回放緩衝時間控制參數：

       此類提供以下工廠方法：
   
   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * 要同時設定初始和播放緩衝時間：

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      如果參數無效，這些方法會擲出`IllegalArgumentException`，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 要設定緩衝區參數值，請使用以下`MediaPlayer`方法：

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 要獲取當前緩衝區參數值，請使用以下`MediaPlayer`方法：

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，若要將初始緩衝區設為2秒，而播放緩衝時間設為30秒：

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

`psdkdemo`展示此功能；使用應用程式的設定來設定緩衝值。
