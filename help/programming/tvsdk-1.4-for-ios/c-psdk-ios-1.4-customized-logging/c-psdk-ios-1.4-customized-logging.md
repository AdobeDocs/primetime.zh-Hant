---
description: 您可以實作您自己的記錄系統。
seo-description: 您可以實作您自己的記錄系統。
seo-title: 自訂記錄
title: 自訂記錄
uuid: c5bdf266-4266-4896-b6e0-47710ce64e67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 自訂記錄 {#customized-logging}

您可以實作您自己的記錄系統。

除了使用預先定義的通知進行記錄外，您還可以建置使用TVSDK產生之記錄訊息和訊息的記錄系統。 如需預先定義通知的詳細資訊，請參 [閱通知系統](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md)。 您可以使用這些記錄檔來疑難排解您的播放器應用程式，並進一步瞭解播放和廣告工作流程。

自訂記錄使用的共用單例例項 `PSDKPTLogFactory`，此例項提供將訊息記錄至多個記錄程式的機制。 您可定義並新增（註冊）一或多個記錄程式至 `PTLogFactory`。 這可讓您使用自訂實作來定義多個記錄程式，例如主控台記錄程式、網頁記錄程式或主控台歷史記錄程式。

TVSDK會針對其許多活動產生記錄訊息，並轉送 `PTLogFactory` 至所有已註冊的記錄程式。 您的應用程式也可以產生自訂記錄訊息，這些訊息會轉送至所有已註冊的記錄程式。 每個記錄程式都可篩選訊息並採取適當動作。

有兩種實施 `PTLogFactory`:

* 用於監聽日誌。
* 用於向添加日誌 `PTLogFactory`。

## 監聽日誌 {#listen-to-logs}

要註冊以監聽日誌：
1. 實作遵循協定的自訂類 `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. 要註冊實例以接收記錄條目，請將實例添加 `PTLogger` 到 `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

以下是使用類型篩選記錄檔的范 `PTLogEntry` 例：

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## 添加新日誌消息 {#add-new-log-messages}

要註冊以監聽日誌：
1. 建立新 `PTLogEntry` 檔案並新增至 `thePTLogFactory`:

   您可以手動實例 `PTLogEntry` 化並將其添加到共用實 `PTLogFactory` 例中，或使用其中一個宏完成相同的任務。

   以下是使用巨集進行記錄的范 `PTLogDebug` 例：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
