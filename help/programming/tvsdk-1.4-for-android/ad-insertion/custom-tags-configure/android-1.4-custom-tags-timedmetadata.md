---
description: 當TVSDK在播放清單/清單中檢測到預訂的標籤時，播放器自動嘗試處理該標籤並以TimedMetadata對象的形式公開它。
title: 定時元資料類
exl-id: d45e304a-703e-45f4-b3f5-756fc6a614cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 定時元資料類{#timed-metadata-class}

當TVSDK在播放清單/清單中檢測到預訂的標籤時，播放器自動嘗試處理該標籤並以TimedMetadata對象的形式公開它。

類提供以下元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 屬性 </th> 
   <th colname="col02" class="entry"> 類型 </th> 
   <th colname="col2" class="entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ID </span> </td> 
   <td colname="col02"> 長 </td> 
   <td colname="col2"> 定時元資料的唯一標識符。 此值通常從提示/標籤ID屬性中提取。 否則，提供唯一隨機值。 使用 <span class="codeph"> getId </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 元資料 </span> </td> 
   <td colname="col02"> 元資料 </td> 
   <td colname="col2"> 從播放清單/清單自定義標籤中處理/提取的資訊。 使用 <span class="codeph"> getMetadata </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 名稱 </span> </td> 
   <td colname="col02"> 字串 </td> 
   <td colname="col2"> 定時元資料的名稱。 如果類型為 <span class="codeph"> 標籤 </span>，值表示提示/標籤名稱。 如果類型為 <span class="codeph"> ID3 </span>，它為空。 使用 <span class="codeph"> getName </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 時間 </span> </td> 
   <td colname="col02"> 長 </td> 
   <td colname="col2"> 相對於主內容開始的時間位置（毫秒），其中流中存在此定時元資料。 使用 <span class="codeph"> getTime </span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 類型 </span> </td> 
   <td colname="col02"> 類型 </td> 
   <td colname="col2"> 定時元資料的類型。 使用 <span class="codeph"> getType </span>。 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG — 表示已根據播放清單/清單中的標籤建立了定時元資料。 </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 — 表示已根據媒體流中的ID3標籤建立了定時元資料。 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

請記住以下內容：

* TVSDK自動將屬性清單提取為鍵值對，並將屬性儲存在元資料屬性中。

   >[!TIP]
   >
   >清單中自定義標籤中的複雜資料（如帶有特殊字元的字串）必須用引號括起來。 例如：
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
   >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果由於自定義標籤格式而提取失敗，則元資料屬性將為空，並且您的應用程式必須提取實際資訊。 在此情況下不引發錯誤。

| 元素 | 說明 |
|---|---|
| `public enum Type { TAG, ID3}` | 定時元資料的可能類型。 |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | 預設建構子（時間是本地流時間）。 |
| `public long getTime();` | 相對於主內容開始的時間位置，在該位置將元資料插入流中。 |
| `public Metadata getMetadata();` | 在流中插入的元資料。 |
| `public Type getType();` | 返回定時元資料的類型。 |
| `public long getId();` | 返回從提示/標籤屬性提取的ID。 否則，提供唯一隨機值。 |
| `public String getName();` | 返回提示的名稱，通常是HLS標籤名稱。 |
