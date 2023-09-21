---
description: 您可以使用NotificationEvent追蹤從Adobe視訊引擎(AVE)傳遞的警告。
title: 追蹤播放器中的AVE警告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 追蹤播放器中的AVE警告{#track-ave-warnings-in-your-player}

您可以使用NotificationEvent追蹤從Adobe視訊引擎(AVE)傳遞的警告。

您的播放器應用程式可以追蹤播放警告和AVE產生的錯誤，例如容錯移轉或網路關閉事件，這些事件不會暫停播放且不需要應用程式採取任何動作。 雖然部分AVE錯誤會由TVSDK處理， `NotificationEvent` 可做為應用程式層的一般傳遞機制，以發出AVE警告。 收到AVE警告後，您可能會選擇採取某些動作，例如主動停止播放、啟用應急計畫、記錄訊息等。

使用下列API元素來追蹤播放器中的AVE警告：

**通知代碼**

```
public final class NotificationCode { 
    /** 
     * Warning message for playback status. 
     */ 
    public static const GENERAL_WARNING:int = 101100; 
}
```

**通知事件**

```
/** 
 * Event dispatched by MediaPlayer when a notification is available 
 * for the current media stream being played. 
 */ 
public class NotificationEvent extends Event { 
    /** 
     * Event dispatched when a new warning has been received for the current item. 
     * 
     * The newly created Notification object can be accessed through  
     * the notification property of this event. 
     */ 
    public static const WARNING_AVAILABLE:String = "warningAvailable"; 
    /** 
     * Helper method for creating NotificationEvent events. 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param notification Associated notification object. 
     * 
     * @return a valid notification event instance. 
     */ 
    public static function create( 
           type:String, notification:Notification):NotificationEvent; 
     /** 
     * Default constructor 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param type           Event type. 
     * @param bubbles        Whether the event can bubble up the display list hierarchy. 
     * @param cancelable     Whether the behavior associated with the event can be prevented. 
     * @param notification   Associated notification object. 
     */ 
    public function NotificationEvent(type:String,  
                                      bubbles:Boolean=false,  
                                      cancelable:Boolean=false,  
                                      notification:Notification= null); 
     /** 
     * The notification associated with this event. 
     */ 
    public function get notification():Notification; 
    /** 
     * @inheritDoc 
     */ 
    public override function clone():Event; 
}
```

將事件接聽程式新增至播放器，以捕捉AVE警告。

例如：

```
var _player:DefaultMediaPlayer = new DefaultMediaPlayer(context); 
_player.addEventListener(NotificationEvent.WARNING_AVAILABLE, onWarningAvailable); 
 
private function onWarningAvailable(event:NotificationEvent):void { 
    var metadata:Metadata = event.notification.metadata; 
    if (metadata != null) { 
        for each (var key:String in metadata.keySet()) { 
            var value:String = metadata.getValue(key); 
            if (!StringUtils.isEmpty(key) && !StringUtils.isEmpty(value)) { 
                _logger.warn("#onWarningAvailable metadata [{0}:{1}]", key, value); 
            } 
        } 
    } 
} 
```

<!--<a id="example_C35262605D394718B40C084B569A5052"></a>-->

以下是使用追蹤的AVE警告範例 `NotificationEvent`：

```
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceType:HLS] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceId:0] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCode:66] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCodeMessage:SEGMENT_SKIPPED_ON_FAILURE] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [eventType:Warning] 
 
<pre>
  [WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [description:url::= 
   https://xyz.corp.adobe.com/pmp/assets/abc/failover/tc.1.04/content/backup-01/ 
   low-res/main-stream4-4x3-info6.ts,periodIndex::=0, 
   sizeBytes::=0,downloadTime(ms)::=0,mediaDuration(ms)::=0] 
</pre>
```
