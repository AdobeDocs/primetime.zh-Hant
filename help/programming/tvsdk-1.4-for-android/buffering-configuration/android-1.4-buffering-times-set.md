---
description: 為了提供更流暢的檢視體驗，TVSDK有時會緩衝視訊資料流。 您可以設定播放器緩衝的方式。
title: 設定緩衝時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 緩衝 {#buffering}

為了提供更流暢的檢視體驗，TVSDK有時會緩衝視訊資料流。 您可以設定播放器緩衝的方式。

TVSDK定義至少30秒的播放緩衝區長度，以及其中在媒體開始播放之前至少2秒的初始緩衝區時間。 應用程式呼叫後 `play` 但在播放開始之前，TVSDK會緩衝媒體至初始時間，以便在媒體實際開始播放時提供順暢的開始。

您可以定義新的緩衝原則來變更緩衝時間，也可以使用立即啟動功能在初始緩衝發生時變更。

## 設定緩衝時間 {#set-buffering-times}

此 `MediaPlayer` 提供設定和取得初始緩衝時間和播放緩衝時間的方法。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝控制引數，媒體播放器預設為初始緩衝為2秒，持續播放緩衝時間則為30秒。

1. 設定 `BufferControlParameters` 物件，封裝初始緩衝時間和播放緩衝時間控制引數：

       此類別提供兩種原廠方法：
   
   * 若要將初始緩衝時間設為等於播放緩衝時間：

     ```java
     public static BufferControlParameters createSimple( 
         long bufferTime)
     ```

   * 若要同時設定初始和播放緩衝時間：

     ```java
     public static BufferControlParameters createDual( 
         long initialBuffer,   
         long bufferTime)
     ```

     這些方法會擲回 `IllegalArgumentException` 如果引數無效，例如：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。

1. 若要設定緩衝區引數值，請使用這個 `MediaPlayer` 方法：

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 若要取得目前的緩衝區引數值，請使用這個 `MediaPlayer` 方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

   如果AVE無法設定指定的值，媒體播放器會輸入 `ERROR` 含有錯誤碼的狀態 `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

例如，若要將初始緩衝設定為2秒，播放緩衝時間設定為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

Primetime參考實作會示範此功能；請使用應用程式的設定來設定緩衝值。
