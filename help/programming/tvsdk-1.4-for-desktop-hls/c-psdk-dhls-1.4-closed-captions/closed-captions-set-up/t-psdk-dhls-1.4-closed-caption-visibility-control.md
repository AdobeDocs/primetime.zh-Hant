---
description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-description: 您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。
seo-title: 控制隱藏字幕的可見度
title: 控制隱藏字幕的可見度
uuid: 360d1158-67d9-40d9-b4b6-8ef46f9d73c0
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 控制隱藏字幕可見度{#control-closed-caption-visibility}

您可以控制隱藏字幕的可見度。 當可見性開啟時，會顯示目前選取的軌道。 如果您變更了目前的軌道，可見度設定會維持不變。

>[!TIP]
>
>如果當播放器進入搜尋模式時顯示隱藏字幕文字，則搜尋完成後不會再顯示文字。 相反地，在數秒後，TVSDK會在結束搜尋位置後，在視訊中顯示下一個隱藏字幕文字。

>[!NOTE]
>
>隱藏字幕的可見度值定義在`ClosedCaptionsVisibility`中。
>
>
```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```

1. 等待`MediaPlayer`至少具有PREPARED狀態（請參閱[等待有效狀態](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)）。
1. 若要取得隱藏字幕的目前可見性設定，請使用`MediaPlayer`中的getter方法，此方法會傳回可見性值。

   ```
   public function get ccVisibility():String
   ```

1. 若要變更隱藏字幕的可見度，請使用setter方法，從`ClosedCaptionsVisibility`傳遞可見度值。

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

1. 定義隱藏字幕軌道的可系結陣列。

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. 設定監聽器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   要從銷毀代碼中刪除監聽程式，請執行以下操作：

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. 當使用者從清單中選擇時，建立並更新清單。

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

