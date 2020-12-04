---
description: 為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器的緩衝方式。
seo-description: 為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器的緩衝方式。
seo-title: 緩衝
title: 緩衝
uuid: c84b98ed-0070-4a86-a409-d7702e5be23c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# 概述{#buffering-overview}

為提供更順暢的檢視體驗，TVSDK有時會緩衝視訊串流。 您可以設定播放器的緩衝方式。

TVSDK定義至少30秒的播放緩衝長度，以及媒體開始播放前的初始緩衝時間，至少2秒。 在應用程式呼叫`play`後，但在播放開始前，TVSDK會將媒體緩衝至初始時間，以便在實際開始播放時提供順暢的開始。

您可以通過定義新的緩衝策略來更改緩衝時間，並且可以通過使用立即啟動來更改初始緩衝的時間。

## 緩衝時間策略{#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

視您的環境（包括裝置、作業系統或網路條件）而定，您可以為播放器設定不同的緩衝原則，例如變更初始緩衝和持續播放緩衝的最短持續時間。

呼叫`play`後，媒體播放器會開始緩衝視訊。 當媒體播放器緩衝了初始緩衝時間所指定的視訊量時，就會開始播放。 此程式可縮短啟動時間，因為播放器不會等到整個播放緩衝區填滿後再開始播放。 而是在緩衝了數秒初始後，開始播放。

在轉譯視訊時，TVSDK會持續緩衝新片段，直到它緩衝播放緩衝時間所指定的量為止。 如果目前的緩衝區長度降到播放緩衝時間以下，播放器將下載其他片段。 當目前的緩衝區長度超過播放緩衝時間數秒後，TVSDK將停止下載片段。

>[!TIP]
>
>如果初始緩衝值很高，則可能會在開始之前為使用者提供較長的初始緩衝時間。 這可能會讓播放更長時間流暢；但是，如果網路條件較差，則可能會延遲初始播放。

如果您透過呼叫`prepareBuffer`來立即啟用，則初始緩衝會從此時開始，而非等待`play`。

## 設定緩衝時間{#section_05CDD927869D47EBA1D2069B1416B2E4}

`MediaPlayer`提供設定和取得初始緩衝時間和播放緩衝時間的方法。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝區控制參數，媒體播放器預設初始緩衝區為2秒，而持續播放緩衝區時間為30秒。

1. 設定`BufferControlParameters`對象，該對象封裝初始緩衝時間和回放緩衝時間控制參數。

   此類提供以下工廠方法：

   * 要將初始緩衝時間設定為等於播放緩衝時間：

      ```
      public static BufferControlParameters createSimple(long bufferTime)
      ```

   * 若要設定初始和播放緩衝時間：

      ```
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```
   如果參數無效，這些方法會擲出`MediaPlayerException`並顯示錯誤代碼`PSDKErrorCode.INVALID_ARGUMENT`，例如當滿足以下條件時：

   * 初始緩衝時間小於零。
   * 初始緩衝時間大於緩衝時間。


1. 要設定緩衝區參數值，請使用以下方法：`MediaPlayer`

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. 要獲取當前緩衝區參數值，請使用以下`MediaPlayer`方法：

   ```java
      BufferControlParameters getBufferControlParameters()  
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

例如，若要將初始緩衝區設為5秒，而播放緩衝區時間設為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
