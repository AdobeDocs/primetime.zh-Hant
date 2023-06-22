---
description: 媒體播放器的狀態會決定哪些動作是合法的。
title: MediaPlayer物件的生命週期和狀態
exl-id: 6b43f334-bd21-4d0e-a123-fd99403a6082
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# MediaPlayer物件的生命週期和狀態 {#lifecycle-and-statuses-of-the-mediaplayer-object}

媒體播放器的狀態會決定哪些動作是合法的。

使用媒體播放器狀態：

* 您可以擷取 `MediaPlayer` 物件與 `MediaPlayer.getStatus()`.

* 狀態清單定義於 [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) 列舉。

生命週期的狀態轉換圖 `MediaPlayer` 例項：
<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

下表提供有關媒體播放器生命週期和狀態的詳細資訊：

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 狀態 </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 閒置 </td> 
   <td colname="col2"> <p>媒體播放器的初始狀態。 播放器已建立，並正等待您指定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 正在初始化 </td> 
   <td colname="col2"> <p>您的應用程式呼叫 <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>正在載入媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 正在準備 </td> 
   <td colname="col2"> <p>您的應用程式呼叫 <span class="codeph"> MediaPlayer.prepareToPlay() </span>. 媒體播放器正在載入媒體播放器專案和任何相關的資源。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已準備 </td> 
   <td colname="col2"> <p>TVSDK已準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 內容已準備好，且廣告已插入時間軸中，或廣告程式失敗。 </p> <p>緩衝或播放可以開始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 正在播放/暫停 </td> 
   <td colname="col2"> <p>當應用程式播放和暫停媒體時，媒體播放器會在這兩種狀態之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已暫停 </td> 
   <td colname="col2"> <p>如果應用程式在播放器播放或暫停時離開播放、關閉裝置或切換應用程式，媒體播放器會暫停並釋放資源。 </p> <p>通話 <span class="codeph"> MediaPlayer.restore() </span> 將播放器傳回至播放器暫停前的狀態。 例外情況是，如果呼叫暫停時播放器正在搜尋，則播放器會暫停然後暫停。 </p> <p>重要：  <p>請記住以下資訊： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">此 <span class="codeph"> MediaPlayer </span> 自動呼叫 <span class="codeph"> 暫停 </span> 只有當使用的曲面物件為 <span class="codeph"> MediaPlayerView </span> 已損毀。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">此 <span class="codeph"> MediaPlayer </span> 自動呼叫 <span class="codeph"> restore() </span> 僅當使用新的曲面物件時 <span class="codeph"> MediaPlayerView </span> 「 」已建立。 </li> 
      </ul> </p> </p> <p>如果您一律想要在MediaPlayer還原時暫停播放，請讓應用程式呼叫 <span class="codeph"> MediaPlayer.pause() </span> 在Android活動的 <span class="codeph"> onPause() </span> 方法。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 完成 </td> 
   <td colname="col2"> <p>播放器已到達串流結尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已發行 </td> 
   <td colname="col2"> <p>您的應用程式已發行媒體播放器，也會發行任何相關資源。 您無法再使用此例項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 錯誤 </td> 
   <td colname="col2"> <p>處理期間發生錯誤。 錯誤也可能會影響應用程式接下來可以執行的動作。 如需詳細資訊，請參閱 <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> 設定錯誤處理 </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供程式的意見回饋，例如，在等待下一個狀態變更時執行微調器，或在播放媒體時採取後續步驟，例如在呼叫下一個方法之前等待適當的狀態。

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
