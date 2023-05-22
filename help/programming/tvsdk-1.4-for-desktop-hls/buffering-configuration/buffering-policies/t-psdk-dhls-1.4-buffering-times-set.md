---
description: MediaPlayer提供設定和獲取初始緩衝時間和回放緩衝時間的方法。
title: 設定緩衝時間
exl-id: d2fbae05-2190-4acc-ae63-561db030608a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 設定緩衝時間{#set-buffering-times}

MediaPlayer提供設定和獲取初始緩衝時間和回放緩衝時間的方法。

>[!TIP]
>
>如果在開始播放之前未設定緩衝區控制參數，則初始緩衝區的媒體播放器預設為2秒，當前播放緩衝區的時間預設為30秒。

1. 設定 `BufferControlParameters` 對象，它封裝了初始緩衝時間和回放緩衝時間控制參數：

       此類提供以下工廠方法：
   
   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```
      createSimple(bufferTime:uint):BufferControlParameters
      ```

   * 要設定初始緩衝時間和播放緩衝時間，請執行以下操作：

      ```
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      ```

      這些方法 `IllegalArgumentException` 如果參數無效，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 要設定緩衝區參數值，請使用 `MediaPlayer` 方法：

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 要獲取當前緩衝區參數值，請使用 `MediaPlayer` 方法：

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，要將初始緩衝區設定為2秒，將回放緩衝區時間設定為30秒：

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

的 `psdkdemo` 演示此功能；使用應用程式的設定設定緩衝區值。
