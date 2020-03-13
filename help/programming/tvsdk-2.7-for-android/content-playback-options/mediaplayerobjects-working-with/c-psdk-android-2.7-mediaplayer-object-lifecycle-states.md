---
description: 媒體播放器的狀態決定哪些動作是合法的。
seo-description: 媒體播放器的狀態決定哪些動作是合法的。
seo-title: MediaPlayer物件的生命週期和狀態
title: MediaPlayer物件的生命週期和狀態
uuid: a0eb27c8-180b-4c56-926f-59fa3bcef032
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# MediaPlayer物件的生命週期和狀態 {#lifecycle-and-statuses-of-the-mediaplayer-object}

媒體播放器的狀態決定哪些動作是合法的。

使用媒體播放器狀態：

* 可以使用檢索對象的當 `MediaPlayer` 前狀態 `MediaPlayer.getStatus()`。

* 狀態清單在 [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) MediaPlayerStatus列舉中定義。

實例生命週期的狀態轉移 `MediaPlayer` 圖：
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
   <td colname="col2"> <p>您的應用程 <span class="codeph"> 式會呼叫MediaPlayer.replaceCurrentItem() </span>。 </p> <p>正在載入媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 準備 </td> 
   <td colname="col2"> <p>您的應用程 <span class="codeph"> 式會呼叫MediaPlayer.prepareToPlay() </span>。 媒體播放器正在載入媒體播放器項目和任何相關資源。 </p> </td> 
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
   <td colname="col2"> <p>如果應用程式在播放或暫停時導覽離開播放、關閉裝置或切換應用程式，媒體播放器就會暫停並釋放資源。 </p> <p>呼叫 <span class="codeph"> MediaPlayer.restore() </span> 會將播放器傳回播放器在暫停前的狀態。 例外情況是，如果呼叫暫停時播放器為SEEKING，則播放器會暫停，然後暫停。 </p> <p>重要：  <p>請記住下列資訊： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">MediaPlayer <span class="codeph"> 只有當MediaPlayerView使用的 </span> 表面物件毀損時，才會自動呼叫「暫停」, <span class="codeph"> MediaPlayer </span><span class="codeph"></span> 會自動呼叫。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">MediaPlayer <span class="codeph"> 僅 </span> 在建立MediaPlayerView所使用的新表面物件時，才會自動呼叫 <span class="codeph"> restore() </span><span class="codeph"></span> 。 </li> 
      </ul> </p> </p> <p>如果您一律想在還原MediaPlayer時暫停播放，請在Android活動的 <span class="codeph"> onPause()方法中，讓應用程式呼叫 </span> MediaPlayer.pause() <span class="codeph"></span> 。 </p> </td> 
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
   <td colname="col2"> <p>進程期間發生錯誤。 錯誤也可能會影響應用程式的下一步動作。 如需詳細資訊，請參 <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> 閱設定錯誤處理 </a>。 </p> </td> 
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

