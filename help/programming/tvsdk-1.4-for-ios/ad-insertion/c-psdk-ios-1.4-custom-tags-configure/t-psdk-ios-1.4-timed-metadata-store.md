---
description: 您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。
seo-description: 您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。
seo-title: 傳送計時中繼資料物件時，可儲存這些物件
title: 傳送計時中繼資料物件時，可儲存這些物件
uuid: d26ed49e-fb29-4765-86e9-9ebbe5fa0a2b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 傳送計時中繼資料物件時，可儲存這些物件 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。

在內容剖析期間（在播放之前）,TVSDK會識別已訂閱的標籤，並通知您的應用程式這些標籤。 與每個時間關聯的時間 `PTTimedMetadata` 是播放時間軸上的絕對時間。

您的應用程式必須完成下列工作：

1. 追蹤目前的播放時間。
1. 將當前播放時間與調度的對象匹 `PTTimedMetadata` 配。

1. 使用開 `PTTimedMetadata` 始時間等於目前播放時間的位置。

   >[!NOTE]
   >
   >以下程式碼假設一次只 `PTTimedMetadata` 有一個例項。 如果有多個例項，應用程式必須將它們正確儲存在字典中。 一種方法是在給定時間建立陣列，並將所有實例儲存在該陣列中。

   以下示例說明如何按每 `PTTimedMetadata` 個的開 `NSMutableDictionary (timedMetadataCollection)` 始時間在鍵中保存對象 `timedMetadata`。

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

## 剖析Nielsen ID3標籤 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

若要擷取ID3標籤以進行剖析，請在方法上使 `onMediaPlayerSubscribedTagIdentified` 用：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

剖析ID3標籤後，請使用下列方式擷取Nielsen特定中繼資料：

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

