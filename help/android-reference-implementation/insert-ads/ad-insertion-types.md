---
description: TVSDK目前提供TVSDK廣告、直接廣告插播和自訂廣告標籤的內建廣告供應商中繼資料支援。
title: 廣告插入類型
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 廣告插入類型{#ad-insertion-types}

TVSDK目前提供TVSDK廣告、直接廣告插播和自訂廣告標籤的內建廣告供應商中繼資料支援。

它支援VOD和即時／線性內容的下列廣告插入工作流程類型。

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 插入類型 </th> 
   <th colname="col2" class="entry"> 支援…… </th> 
   <th colname="col3" class="entry"> 說明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Adobe Primetime廣告決策廣告 </td> 
   <td colname="col2">VOD <p>即時 </p> <p>線性 </p> </td> 
   <td colname="col3">參考實作根據JSON設定檔案</a>的Primetime廣告部分</a>中提供的資訊，提供<span class="codeph"> AuditudeMetadata</span>資訊，以連線至伺服器以進行Primetime廣告決策（先前稱為Auditude）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接廣告插播 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">您必須在輸入JSON檔案中提供廣告URL。 當TVSDK嘗試解析廣告時，會呼叫直接廣告分段解析程式，並根據JSON設定檔案</a>中提供的直接廣告分段資訊來解析廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自訂廣告標籤 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">當視訊串流同時包含主要內容和廣告，但不包含與廣告位置和時間相關的資訊時，自訂廣告標籤很有用。 如果以其他方式取得廣告定位資訊，例如透過外部CMS，您可以定義自訂廣告標籤，並將其傳遞至播放器時間軸。 <p>若要設定廣告插入的播放器，您必須在JSON設定檔案</a>的自訂廣告中繼資料區段中傳遞廣告中繼資料，該設定檔案在參考實作中具有支援廣告提供者實作。 </p> </td>
  </tr>
 </tbody>
</table>