---
description: 您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。
title: 控制隱藏式字幕可視性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 控制隱藏式字幕可視性{#control-closed-caption-visibility}

您可以控制隱藏式字幕的可見度。 當可見度開啟時，會顯示目前選取的軌道。 如果變更目前哪個軌跡，可視性設定會保持相同。

>[!TIP]
>
>如果在播放器進入搜尋模式時顯示隱藏式字幕文字，搜尋完成後文字將不再顯示。 相反地，幾秒後，TVSDK會在視訊中搜尋結束位置後顯示下一個隱藏式字幕文字。

>[!NOTE]
>
>隱藏式字幕的可見度值定義於 `ClosedCaptionsVisibility`.
>
>```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```
>

1. 等待 `MediaPlayer` 至少要有「已準備」狀態(請參閱 [等待有效的狀態](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md))。
1. 若要取得隱藏式字幕的目前可見度設定，請在中使用getter方法 `MediaPlayer`，會傳回可見度值。

   ```
   public function get ccVisibility():String
   ```

1. 若要變更隱藏式字幕的可見度，請使用setter方法，傳遞可視度值 `ClosedCaptionsVisibility`.

   例如：

   ```
   public function set ccVisibility(value:String):void
   ```

1. 定義下拉式清單。

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. 定義隱藏式字幕軌跡的可繫結陣列。

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. 設定監聽器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   若要將監聽器從您的銷毀程式碼中移除：

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. 當使用者從清單進行選擇時建立和更新清單。

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```
