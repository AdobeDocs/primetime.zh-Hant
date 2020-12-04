---
description: 您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。
seo-description: 您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。
seo-title: 傳送計時中繼資料物件時，可儲存這些物件
title: 傳送計時中繼資料物件時，可儲存這些物件
uuid: 38e72a9b-571a-48da-9c17-80be453e6a98
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 將計時的中繼資料物件傳送至{#store-timed-metadata-objects-as-they-are-dispatched}時儲存

您的應用程式必須在適當的時間使用適當的PTTimedMetadata物件。

在內容剖析期間（在播放之前）,TVSDK會識別已訂閱的標籤，並通知您的應用程式這些標籤。 與每個`PTTimedMetadata`相關聯的時間是播放時間軸上的絕對時間。

您的應用程式必須完成下列工作：

1. 追蹤目前的播放時間。
1. 將當前播放時間與已調度的`PTTimedMetadata`對象匹配。

1. 使用`PTTimedMetadata`，其中開始時間等於目前播放時間。

   >[!NOTE]
   >
   >下面的代碼假定一次只有一個`PTTimedMetadata`實例。 如果有多個例項，應用程式必須將它們正確儲存在字典中。 一種方法是在給定時間建立陣列，並將所有實例儲存在該陣列中。

   以下示例說明如何按每個`timedMetadata`的開始時間將`PTTimedMetadata`對象保存在`NSMutableDictionary (timedMetadataCollection)`鍵中。

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

## 剖析Nielsen ID3標籤{#example_3B51E9D4AF2449FAA8E804206F873ECF}

若要擷取ID3標籤以進行剖析，請在`onMediaPlayerSubscribedTagIdentified`方法上使用下列：

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
