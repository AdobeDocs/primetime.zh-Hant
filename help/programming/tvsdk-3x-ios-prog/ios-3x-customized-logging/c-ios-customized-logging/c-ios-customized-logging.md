---
description: 您可以實作自己的記錄系統。
title: 瞭解自訂記錄
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 自訂記錄 {#customized-logging}

您可以實作自己的記錄系統。

除了使用預先定義的通知來記錄外，您還可以實作記錄系統，此系統使用TVSDK產生的記錄訊息和訊息。 如需預先定義通知的詳細資訊，請參閱 [通知系統](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System). 您可以使用這些記錄檔來疑難排解播放器應用程式，以及提供對播放和廣告工作流程更深入的瞭解。

自訂記錄使用下列專案的共用單一例項： `PSDKPTLogFactory`，提供將訊息記錄到多個記錄器的機制。 您可以定義並新增（註冊）一或多個記錄器至 `PTLogFactory`. 這可讓您使用自訂實施來定義多個記錄器，例如主控台記錄器、網頁記錄器或主控台歷史記錄記錄器。

TVSDK會產生許多活動的記錄訊息，這些活動 `PTLogFactory` 轉寄給所有已註冊的記錄器。 您的應用程式也可以產生自訂記錄訊息，這些訊息會轉送給所有已註冊的記錄器。 每個記錄器都可以篩選訊息並採取適當的動作。

有兩個針對的實作 `PTLogFactory`：

* 用於聆聽記錄。
* 用於將記錄新增至 `PTLogFactory`.

## 聆聽記錄 {#listen-to-logs}

若要登入以監聽記錄檔：
1. 實作遵循通訊協定的自訂類別 `PTLogger`：

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

1. 若要註冊執行處理以接收記錄專案，請新增執行處理的 `PTLogger` 至 `PTLoggerFactory`：

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

以下範例說明如何使用 `PTLogEntry` 型別：

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

## 新增記錄訊息 {#add-new-log-messages}

若要註冊以監聽記錄檔：

建立新的 `PTLogEntry` 並將其新增至 `thePTLogFactory`：

您可以手動具現化 `PTLogEntry` 並將其新增至 `PTLogFactory` 共用實體或使用其中一個巨集完成相同工作。

以下是使用的記錄範例 `PTLogDebug` 巨集：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
