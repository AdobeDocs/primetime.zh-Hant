---
description: MediaPlayer提供方法來設定及取得初始緩衝時間和播放緩衝時間。
title: 設定緩衝時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# 設定緩衝時間{#set-buffering-times}

MediaPlayer提供方法來設定及取得初始緩衝時間和播放緩衝時間。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝控制引數，媒體播放器預設為初始緩衝為2秒，持續播放緩衝時間則為30秒。

1. 設定 `BufferControlParameters` 物件，封裝初始緩衝時間和播放緩衝時間控制引數：

       此類別提供下列原廠方法：
   
   * 若要將初始緩衝時間設為等於播放緩衝時間：

     ```
     createSimple(bufferTime:uint):BufferControlParameters
     ```

   * 若要同時設定初始和播放緩衝時間：

     ```
     createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
     ```

     這些方法會擲回 `IllegalArgumentException` 如果引數無效，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 若要設定緩衝區引數值，請使用這個 `MediaPlayer` 方法：

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. 若要取得目前的緩衝區引數值，請使用這個 `MediaPlayer` 方法：

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，若要將初始緩衝設定為2秒，播放緩衝時間設定為30秒：

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

此 `psdkdemo` 示範此功能；使用應用程式的設定來設定緩衝值。
