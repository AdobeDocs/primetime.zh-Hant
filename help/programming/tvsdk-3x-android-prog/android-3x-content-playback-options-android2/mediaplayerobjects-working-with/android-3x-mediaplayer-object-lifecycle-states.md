---
description: 媒體播放器的狀態決定哪些動作是合法的。
title: MediaPlayer物件的生命週期和狀態
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# MediaPlayer物件的生命週期和狀態{#lifecycle-and-statuses-of-the-mediaplayer-object}

媒體播放器的狀態決定哪些動作是合法的。

使用媒體播放器狀態：

* 可以使用`MediaPlayer.getStatus()`檢索`MediaPlayer`對象的當前狀態。

* 狀態清單在[MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html)列舉中定義。

`MediaPlayer`實例生命週期的狀態轉移圖：

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

下表提供媒體播放器生命週期和狀態的詳細資訊：

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 狀態 </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 空閒 </td> 
   <td colname="col2"> <p>媒體播放器的初始狀態。 播放器已建立，且正等您指定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 初始化 </td> 
   <td colname="col2"> <p>您的應用程式會呼叫<span class="codeph"> MediaPlayer.replaceCurrentItem()</span>。 </p> <p>正在載入媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 準備 </td> 
   <td colname="col2"> <p>您的應用程式會呼叫<span class="codeph"> MediaPlayer.prepareToPlay()</span>。 媒體播放器正在載入媒體播放器項目和任何相關資源。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 準備好 </td> 
   <td colname="col2"> <p>TVSDK已準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 內容已準備好，廣告已插入時間軸，或廣告程式失敗。 </p> <p>可以開始緩衝或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 播放／暫停 </td> 
   <td colname="col2"> <p>當應用程式播放和暫停媒體時，媒體播放器會在這些狀態之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已暫停 </td> 
   <td colname="col2"> <p>如果應用程式在播放或暫停時導覽離開播放、關閉裝置或切換應用程式，媒體播放器就會暫停並釋放資源。 </p> <p>呼叫<span class="codeph"> MediaPlayer.restore()</span>會將播放器傳回播放器暫停前的狀態。 例外情況是，如果呼叫暫停時播放器為SEEKING，則播放器會暫停，然後暫停。 </p> <p>重要：  <p>請記住下列資訊： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C"><span class="codeph"> MediaPlayer </span>只有當<span class="codeph"> MediaPlayerView </span>所使用的表面物件毀損時，才會自動呼叫<span class="codeph">暫停</span>。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1"><span class="codeph"> MediaPlayer </span>僅在<span class="codeph"> MediaPlayerView </span>使用的新曲面物件建立時，才會自動呼叫<span class="codeph"> restore()</span>。 </li> 
      </ul> </p> </p> <p>如果您一律想在還原MediaPlayer時暫停播放，請在Android活動的<span class="codeph"> onPause()</span>方法中，讓您的應用程式呼叫<span class="codeph"> MediaPlayer.pause()</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 完成 </td> 
   <td colname="col2"> <p>播放器已到達串流的尾端，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已發佈 </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，而媒體播放器也會發佈任何相關資源。 您無法再使用此例項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 錯誤 </td> 
   <td colname="col2"> <p>進程期間發生錯誤。 錯誤也可能會影響應用程式的下一步動作。 如需詳細資訊，請參閱<a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local">設定錯誤處理</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關程式的反饋，或者例如，在等待下一個狀態更改時提供微調器，或在播放媒體時採取後續步驟，例如在呼叫下一個方法之前等待適當的狀態。

例如：

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
