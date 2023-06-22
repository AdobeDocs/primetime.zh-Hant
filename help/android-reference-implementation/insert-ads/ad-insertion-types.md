---
description: TVSDK目前為TVSDK廣告、直接廣告插播和自訂廣告標籤提供內建廣告提供者中繼資料支援。
title: 廣告插入型別
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 廣告插入型別 {#ad-insertion-types}

TVSDK目前為TVSDK廣告、直接廣告插播和自訂廣告標籤提供內建廣告提供者中繼資料支援。

它支援下列VOD和即時/線性內容的廣告插入工作流程型別。

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 插入型別 </th> 
   <th colname="col2" class="entry"> 支援…… </th> 
   <th colname="col3" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime ad decisioning ads </td> 
   <td colname="col2">VOD <p>即時 </p> <p>線性 </p> </td> 
   <td colname="col3">參考實作提供 <span class="codeph"> AuditudeMetadata</span> 根據Primetime廣告部分提供的資訊，連線到伺服器以進行Primetime廣告決策（先前稱為Auditude）的資訊</a> JSON設定檔案的</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接廣告插播 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">您必須在輸入JSON檔案中提供廣告URL。 當TVSDK嘗試解析廣告時，會呼叫直接廣告插播解析器，並根據JSON設定檔案中提供的直接廣告插播資訊來解析廣告</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自訂廣告標籤 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">當視訊串流同時包含主要內容和廣告，但不包含與廣告位置和時間相關的資訊時，自訂廣告標籤很有用。 如果廣告定位資訊是以其他方式取得（例如透過外部CMS），您可以定義自訂廣告標籤，並將其傳遞給播放器時間軸。 <p>若要設定廣告插入的播放器，您需要在JSON設定檔案的自訂廣告中繼資料區段中傳遞廣告中繼資料</a>，在參考實作中具有支援的廣告提供者實作。 </p> </td>
  </tr>
 </tbody>
</table>
