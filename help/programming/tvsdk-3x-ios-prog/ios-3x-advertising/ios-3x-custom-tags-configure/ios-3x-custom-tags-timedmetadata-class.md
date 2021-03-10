---
description: 當TVSDK偵測到播放清單／資訊清單中的訂閱標籤時，播放器會自動嘗試處理標籤並以PTTimedMetadata物件的形式公開標籤。
title: 計時中繼資料類別
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# 計時中繼資料類別{#timed-metadata-class}

當TVSDK偵測到播放清單／資訊清單中的訂閱標籤時，播放器會自動嘗試處理標籤並以PTTimedMetadata物件的形式公開標籤。

該類提供以下元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>屬性</b></th> 
   <th colname="col02" class="entry"><b>類型</b> </th> 
   <th colname="col2" class="entry"><b>說明</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> 計時中繼資料的唯一識別碼。 此值通常從cue/tag ID屬性中擷取。 否則，提供唯一隨機值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 名稱</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> 計時中繼資料的名稱。 如果類型為<span class="codeph"> TAG</span>，則值代表提示／標籤名稱。 如果類型為<span class="codeph"> ID3</span>，則為null。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 時間</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> 相對於主要內容開始的時間位置（以毫秒為單位），在主要內容開始時，此計時中繼資料會出現在串流中。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">計時中繼資料的類型。 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG —— 指出計時中繼資料是從播放清單／資訊清單中的標籤建立。 </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 —— 表示計時中繼資料是從媒體串流的ID3標籤建立。 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

請記住：

* TVSDK會自動將屬性清單擷取為索引鍵值配對，並將屬性儲存在中繼資料屬性中。

   >[!TIP]
   >
   >資訊清單中自訂標籤中的複雜資料（例如含特殊字元的字串）必須使用引號。 例如：
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果擷取因自訂標籤格式而失敗，內容屬性一律會包含標籤的原始資料，即冒號後的字串。 此情況下不會擲回錯誤。

| **元素** | **說明** |
|---|---|
| TAG, ID3 | 計時中繼資料的可能類型。 |
| `@property (nonatomic, assign) CMTime time` | 相對於主要內容開始的時間位置，此元資料插入到流中。 |
| `@property (nonatomic, assign) PTTimedMetadataType type` | 傳回計時中繼資料的類型。 |
| `@property (nonatomic, retain) NSString *metadataId` | 傳回從提示／標籤屬性擷取的ID。 否則，提供唯一隨機值。 |
| `@property (nonatomic, retain) NSString *name` | 傳回提示的名稱，此名稱通常為HLS標籤名稱。 |