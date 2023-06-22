---
description: 您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。
title: 在傳送定時中繼資料物件時將其儲存
exl-id: 43bc2b47-b947-4af1-bba8-6f2063c7b60c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 在傳送定時中繼資料物件時將其儲存 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。

在內容剖析期間（發生在播放之前），TVSDK會識別訂閱的標籤，並通知您的應用程式這些標籤。 與每個報表套裝相關聯的時間 `PTTimedMetadata` 是播放時間軸的絕對時間。

您的應用程式必須完成下列工作：

1. 追蹤目前的播放時間。
1. 比對目前播放時間與已傳送的時間 `PTTimedMetadata` 物件。

1. 使用 `PTTimedMetadata` 其中開始時間等於目前播放時間。

   >[!NOTE]
   >
   >以下程式碼假設只有一個 `PTTimedMetadata` 一次執行個體。 如果有多個執行個體，應用程式必須適當地儲存在字典中。 一種方法是在指定時間建立陣列，並儲存該陣列中的所有執行個體。

   以下範例說明如何儲存 `PTTimedMetadata` 中的物件 `NSMutableDictionary (timedMetadataCollection)` 以每個專案的開始時間作為索引鍵 `timedMetadata`.

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

若要擷取ID3標籤以供剖析，請在 `onMediaPlayerSubscribedTagIdentified` 方法：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

剖析ID3標籤後，請使用下列專案擷取Nielsen專屬的中繼資料：

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
