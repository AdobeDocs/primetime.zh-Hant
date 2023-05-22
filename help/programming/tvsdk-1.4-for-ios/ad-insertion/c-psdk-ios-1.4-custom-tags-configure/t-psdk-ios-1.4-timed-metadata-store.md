---
description: 您的應用程式必須在適當的時間使用相應的PTTimedMetadata對象。
title: 在調度時儲存定時元資料對象
exl-id: 43bc2b47-b947-4af1-bba8-6f2063c7b60c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 在調度時儲存定時元資料對象 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用相應的PTTimedMetadata對象。

在內容分析期間（在播放之前）,TVSDK識別訂閱的標籤並將這些標籤通知您的應用程式。 與每個關聯的時間 `PTTimedMetadata` 是播放時間線上的絕對時間。

您的應用程式必須完成以下任務：

1. 跟蹤當前播放時間。
1. 將當前播放時間與已調度時間匹配 `PTTimedMetadata` 對象。

1. 使用 `PTTimedMetadata` 其中，開始時間等於當前回放時間。

   >[!NOTE]
   >
   >以下代碼假定只有一個 `PTTimedMetadata` 實例。 如果有多個實例，應用程式必須將它們正確保存在字典中。 一種方法是在給定時間建立陣列並將所有實例儲存在該陣列中。

   以下示例說明如何保存 `PTTimedMetadata` 對象 `NSMutableDictionary (timedMetadataCollection)` 由每個的開始時間鍵控 `timedMetadata`。

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## 解析尼爾森ID3標籤 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

要提取ID3標籤以進行分析，請在 `onMediaPlayerSubscribedTagIdentified` 方法：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

分析ID3標籤後，使用以下方法提取特定於尼爾森的元資料：

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
