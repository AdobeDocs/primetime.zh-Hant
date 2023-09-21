---
description: 為了提供更流暢的檢視體驗，TVSDK有時會緩衝視訊資料流。 您可以設定播放器緩衝的方式。
title: 緩衝
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 概觀 {#buffering-overview}

為了提供更流暢的檢視體驗，TVSDK有時會緩衝視訊資料流。 您可以設定播放器緩衝的方式。

TVSDK定義播放緩衝區長度至少30秒，以及媒體開始播放前的初始緩衝時間（至少2秒）。 應用程式呼叫後 `play`，但在播放開始前，TVSDK會緩衝媒體，直到初始時間，以便在媒體實際開始播放時提供順暢的開始。

您可以定義新的緩衝原則來變更緩衝時間，也可以使用立即開啟來變更初始緩衝發生時的時間。

## 緩衝時間原則 {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

根據您的環境（包括裝置、作業系統或網路條件），您可以為播放器設定不同的緩衝原則，例如變更初始緩衝和持續播放緩衝的最短持續時間。

在您呼叫之後 `play`，媒體播放器會開始緩衝視訊。 當媒體播放器已緩衝由初始緩衝時間指定的視訊量時，就會開始播放。 此程式可改善啟動時間，因為播放器不會等待整個播放緩衝區填滿後再開始播放。 相反地，在緩衝了幾個初始秒數後，開始播放。

呈現視訊時，TVSDK會繼續緩衝新片段，直到緩衝播放緩衝時間所指定的量為止。 如果目前的緩衝長度低於播放緩衝時間，播放器會下載其他片段。 一旦目前的緩衝區長度超過播放緩衝區時間幾秒鐘，TVSDK就會停止下載片段。

>[!TIP]
>
>如果初始緩衝值很高，可能會讓使用者在開始前有較長的初始緩衝時間。 這樣可以提供較長的流暢播放時間；但是，如果網路條件很差，則初始播放可能會延遲。

如果您透過呼叫啟用立即開啟 `prepareBuffer`，初始緩衝此時開始，而不是等待 `play`.

## 設定緩衝時間 {#section_05CDD927869D47EBA1D2069B1416B2E4}

此 `MediaPlayer` 提供設定和取得初始緩衝時間和播放緩衝時間的方法。

>[!TIP]
>
>如果您在開始播放之前未設定緩衝控制引數，媒體播放器預設為初始緩衝為2秒，持續播放緩衝時間則為30秒。

1. 設定 `BufferControlParameters` 物件，可封裝初始緩衝時間和播放緩衝時間控制引數。

   此類別提供下列原廠方法：

   * 若要將初始緩衝時間設為等於播放緩衝時間：

     ```
     public static BufferControlParameters createSimple(long bufferTime)
     ```

   * 若要設定初始和播放緩衝時間：

     ```
     public static BufferControlParameters createDual( 
       long initialBuffer,  
       long bufferTime)
     ```

   如果引數無效，這些方法會擲回 `MediaPlayerException` 含錯誤碼 `PSDKErrorCode.INVALID_ARGUMENT`，例如當符合下列條件時：

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

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

例如，若要將初始緩衝設定為5秒，播放緩衝時間設定為30秒：

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
