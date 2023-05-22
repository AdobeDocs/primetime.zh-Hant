---
description: 為了提供更流暢的觀看體驗，TVSDK有時會緩衝視頻流。 您可以配置播放器緩衝的方式。
title: 緩衝
exl-id: 3b706420-878d-487a-8db7-cff2a12c2660
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 概述 {#buffering-overview}

為了提供更流暢的觀看體驗，TVSDK有時會緩衝視頻流。 您可以配置播放器緩衝的方式。

TVSDK定義至少30秒的播放緩衝長度和至少2秒的媒體開始播放之前的初始緩衝時間。 應用程式調用後 `play`，但是在播放開始之前，TVSDK會將媒體緩衝到初始時間，以便在實際開始播放時提供平滑的開始。

您可以通過定義新的緩衝策略來更改緩衝時間，也可以通過使用「即時」來更改初始緩衝時間。

## 緩衝時間策略 {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

根據您的環境（包括設備、作業系統或網路條件），您可以為播放器設定不同的緩衝策略，例如更改初始緩衝和持續播放緩衝的最短持續時間。

打電話後 `play`，媒體播放器開始緩衝視頻。 當媒體播放器緩衝了由初始緩衝時間指定的視頻量時，播放開始。 此過程可縮短啟動時間，因為播放器在開始播放之前不會等待整個播放緩衝區填充。 相反，在緩衝幾個初始秒後，開始回放。

在呈現視頻時，TVSDK繼續緩衝新片段，直到它緩衝了由播放緩衝時間指定的量。 如果當前緩衝區長度低於播放緩衝區時間，則播放器將下載其他片段。 當當前緩衝區長度超過播放緩衝區時間幾秒鐘後，TVSDK將停止下載片段。

>[!TIP]
>
>如果初始緩衝區值較高，則可能會在啟動之前給用戶較長的初始緩衝時間。 這可能會在更長的時間內提供平穩回放；但是，如果網路條件較差，則可能會延遲初始回放。

如果通過呼叫啟用即時 `prepareBuffer`，初始緩衝在此時開始，而不是等待 `play`。

## 設定緩衝時間 {#section_05CDD927869D47EBA1D2069B1416B2E4}

的 `MediaPlayer` 提供了設定和獲取初始緩衝時間和回放緩衝時間的方法。

>[!TIP]
>
>如果在開始播放之前未設定緩衝區控制參數，則初始緩衝區的媒體播放器預設為2秒，當前播放緩衝區的時間預設為30秒。

1. 設定 `BufferControlParameters` 對象，它封裝了初始緩衝時間和回放緩衝時間控制參數。

   此類提供以下工廠方法：

   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 要設定初始和播放緩衝時間：

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   如果參數無效，則這些方法將拋出 `MediaPlayerException` 錯誤代碼 `PSDKErrorCode.INVALID_ARGUMENT`，例如：

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

例如，要將初始緩衝區設定為5秒，將回放緩衝區時間設定為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
