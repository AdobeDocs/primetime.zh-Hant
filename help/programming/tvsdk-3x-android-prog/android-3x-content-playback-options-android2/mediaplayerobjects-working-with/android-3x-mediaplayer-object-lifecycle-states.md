---
description: 媒體播放器的狀態確定哪些操作是合法的。
title: MediaPlayer對象的生命週期和狀態
exl-id: b50d5378-4e9b-44c0-9098-8c3e27053b3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# MediaPlayer對象的生命週期和狀態{#lifecycle-and-statuses-of-the-mediaplayer-object}

媒體播放器的狀態確定哪些操作是合法的。

使用媒體播放器狀態：

* 可以檢索 `MediaPlayer` 對象 `MediaPlayer.getStatus()`。

* 狀態清單在 [媒體播放器狀態](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) 枚舉。

生命週期的狀態轉換圖 `MediaPlayer` 實例：

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

下表提供了有關媒體播放器的生命週期和狀態的詳細資訊：

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 狀態 </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 空閒 </td> 
   <td colname="col2"> <p>媒體播放器的初始狀態。 播放器已建立，並正在等待您指定媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 初始化 </td> 
   <td colname="col2"> <p>您的應用程式調用 <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>。 </p> <p>正在載入媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已初始化 </td> 
   <td colname="col2"> <p>TVSDK成功設定媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 準備 </td> 
   <td colname="col2"> <p>您的應用程式調用 <span class="codeph"> MediaPlayer.prepareToPlay() </span>。 媒體播放器正在載入媒體播放器項目和任何相關的資源。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 準備 </td> 
   <td colname="col2"> <p>TVSDK已準備媒體流，並嘗試執行廣告解析和廣告插入（如果啟用）。 準備內容並將廣告插入時間軸，或廣告過程失敗。 </p> <p>可以開始緩衝或回放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 播放/暫停 </td> 
   <td colname="col2"> <p>當應用程式播放和暫停媒體時，媒體播放器在這些狀態之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 掛起 </td> 
   <td colname="col2"> <p>如果應用程式在播放器正在播放或暫停時導航離開重放、關閉設備或切換應用程式，則媒體播放器被掛起並釋放資源。 </p> <p>呼叫 <span class="codeph"> MediaPlayer.restore() </span> 將玩家返回到玩家處於SUSPENDED之前的狀態。 例外情況是，當調用掛起時，如果播放器為SEEKING，則播放器為PUASED，然後為SUSPENDED。 </p> <p>重要提示：  <p>記住以下資訊： 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">的 <span class="codeph"> 媒體播放器 </span> 自動呼叫 <span class="codeph"> 暫停 </span> 僅當由 <span class="codeph"> 媒體播放器視圖 </span> 被毀。 </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">的 <span class="codeph"> 媒體播放器 </span> 自動呼叫 <span class="codeph"> 還原() </span> 僅當由 <span class="codeph"> 媒體播放器視圖 </span> 的子菜單。 </li> 
      </ul> </p> </p> <p>如果在恢復MediaPlayer時始終希望暫停播放，請讓應用程式調用 <span class="codeph"> MediaPlayer.pause() </span> 在Android Activity中 <span class="codeph"> onPause() </span> 的雙曲餘切值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 完成 </td> 
   <td colname="col2"> <p>播放器已到達流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已發佈 </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，該播放器還會釋放任何相關的資源。 您不能再使用此實例。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 錯誤 </td> 
   <td colname="col2"> <p>進程期間出錯。 錯誤還可能影響應用程式接下來可以執行的操作。 有關詳細資訊，請參見 <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> 設定錯誤處理 </a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關進程的反饋，例如，在等待下一個狀態更改時提供反饋，或在播放媒體時採取後續步驟，例如在調用下一個方法之前等待適當的狀態。

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
