---
description: 當TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並以TimedMetadata物件的形式將其公開。
title: 定時中繼資料類別
exl-id: d45e304a-703e-45f4-b3f5-756fc6a614cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 定時中繼資料類別{#timed-metadata-class}

當TVSDK偵測到播放清單/資訊清單中有訂閱的標籤時，播放器會自動嘗試處理該標籤，並以TimedMetadata物件的形式將其公開。

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
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> 計時中繼資料的唯一識別碼。 此值通常擷取自提示/標籤ID屬性。 否則，會提供唯一的隨機值。 使用 <span class="codeph"> getId </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 中繼資料 </span> </td> 
   <td colname="col02"> 中繼資料 </td> 
   <td colname="col2"> 從播放清單/資訊清單自訂標籤中處理/擷取的資訊。 使用 <span class="codeph"> getMetadata </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 名稱 </span> </td> 
   <td colname="col02"> 字串 </td> 
   <td colname="col2"> 計時中繼資料的名稱。 如果型別是 <span class="codeph"> 標籤 </span>，值代表提示/標籤名稱。 如果型別是 <span class="codeph"> ID3 </span>，為null。 使用 <span class="codeph"> getName </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 時間 </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> 相對於主要內容開始的時間位置（以毫秒為單位），此計時中繼資料會出現在資料流中。 使用 <span class="codeph"> getTime </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> 型別 </td> 
   <td colname="col2"> 計時中繼資料的型別。 使用 <span class="codeph"> getType </span>. 
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
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
   >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果擷取因自訂標籤格式而失敗，中繼資料屬性將為空白，且您的應用程式必須擷取實際資訊。 在此情況下不會擲回任何錯誤。

| 元素 | 說明 |
|---|---|
| `public enum Type { TAG, ID3}` | 計時中繼資料的可能型別。 |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | 預設建構函式（time是本機資料流時間）。 |
| `public long getTime();` | 相對於主要內容開頭的時間位置，此中繼資料插入資料流中的位置。 |
| `public Metadata getMetadata();` | 插入串流的中繼資料。 |
| `public Type getType();` | 傳回計時中繼資料的型別。 |
| `public long getId();` | 傳回從提示/標籤屬性擷取的ID。 否則，會提供唯一的隨機值。 |
| `public String getName();` | 傳回提示的名稱，通常是HLS標籤名稱。 |
