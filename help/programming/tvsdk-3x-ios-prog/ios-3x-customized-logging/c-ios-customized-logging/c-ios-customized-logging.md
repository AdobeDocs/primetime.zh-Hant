---
description: 您可以實現自己的日誌記錄系統。
title: 瞭解自定義日誌記錄
exl-id: 8b6a916e-783e-40e1-8a3d-706b57a6ff63
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 自定義日誌記錄 {#customized-logging}

您可以實現自己的日誌記錄系統。

除了使用預定義通知進行記錄外，您還可以實現使用TVSDK生成的日誌消息和消息的記錄系統。 有關預定義通知的詳細資訊，請參閱 [通知系統](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System)。 您可以使用這些日誌來排除播放器應用程式的故障，並更好地瞭解播放和廣告工作流。

自定義日誌記錄使用的共用單個實例 `PSDKPTLogFactory`，它提供了一種機制，可將消息記錄到多個記錄程式。 您可以定義並向 `PTLogFactory`。 這允許您使用自定義實現定義多個記錄器，如控制台記錄器、Web記錄器或控制台歷史記錄記錄器。

TVSDK為其許多活動生成日誌消息， `PTLogFactory` 轉發給所有已註冊的記錄程式。 您的應用程式還可以生成自定義日誌消息，這些消息將轉發給所有已註冊的日誌程式。 每個記錄器都可以過濾消息並採取適當的操作。

有兩種實現 `PTLogFactory`:

* 用於監聽日誌。
* 將日誌添加到 `PTLogFactory`。

## 偵聽日誌 {#listen-to-logs}

要註冊以偵聽日誌，請執行以下操作：
1. 實現遵循協定的自定義類 `PTLogger`:

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

1. 要註冊實例以接收日誌記錄條目，請添加 `PTLogger` 到 `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

下面是使用 `PTLogEntry` 類型：

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

要註冊以偵聽日誌，請執行以下操作：

新建 `PTLogEntry` 並添加到 `thePTLogFactory`:

可以手動實例化 `PTLogEntry` 並加到 `PTLogFactory` 共用實例或使用其中一個宏完成同一任務。

下面是使用 `PTLogDebug` 宏：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
