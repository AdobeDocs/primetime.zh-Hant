---
description: 當TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並以PTTimedMetadata物件的形式將其公開。
title: 定時中繼資料類別
exl-id: b619b019-cb6d-4c31-a7e2-7ebe2f44a4b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 定時中繼資料類別{#timed-metadata-class}

當TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並以PTTimedMetadata物件的形式將其公開。

類別提供下列元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性 </th> 
   <th colname="col02" class="entry"> 型別 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> 計時中繼資料的唯一識別碼。 此值通常擷取自提示/標籤ID屬性。 否則，會提供唯一的隨機值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 名稱</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> 計時中繼資料的名稱。 如果型別是 <span class="codeph"> 標籤</span>，值代表提示/標籤名稱。 如果型別是 <span class="codeph"> ID3</span>，為null。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 時間</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> 相對於主要內容開始的時間位置（以毫秒為單位），此計時中繼資料會出現在資料流中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">計時中繼資料的型別。 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG — 表示計時中繼資料是從播放清單/資訊清單中的標籤建立的。 </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 — 表示計時中繼資料是從媒體資料流中的ID3標籤建立的。 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

請記住以下事項：

* TVSDK會自動將屬性清單擷取到索引鍵/值組中，並將屬性儲存在中繼資料屬性中。

   >[!TIP]
   >
   >資訊清單中自訂標籤內的複雜資料（例如具有特殊字元的字串）必須用引號括住。 例如：
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果擷取因自訂標籤格式而失敗，內容屬性一律包含標籤的原始資料，也就是冒號後的字串。 在此情況下不會擲回任何錯誤。

| 元素 | 說明 |
|---|---|
| 標籤， ID3 | 計時中繼資料的可能型別。 |
| `@property (nonatomic, assign) CMTime time` | 相對於主要內容開頭的時間位置，此中繼資料插入資料流中的位置。 |
| `@property (nonatomic, assign) PTTimedMetadataType type` | 傳回計時中繼資料的型別。 |
| `@property (nonatomic, retain) NSString *metadataId` | 傳回從提示/標籤屬性擷取的ID。 否則，會提供唯一的隨機值。 |
| `@property (nonatomic, retain) NSString *name` | 傳回提示的名稱，通常是HLS標籤名稱。 |
