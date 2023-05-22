---
description: TVSDK當前為TVSDK廣告、直接廣告中斷和自定義廣告標籤提供內置廣告提供商元資料支援。
title: 廣告插入類型
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 廣告插入類型 {#ad-insertion-types}

TVSDK當前為TVSDK廣告、直接廣告中斷和自定義廣告標籤提供內置廣告提供商元資料支援。

它支援以下類型的廣告插入工作流，用於視頻點播和即時/線性內容。

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
   <td colname="col1"> Adobe Primetime廣告決策 </td> 
   <td colname="col2">視頻點播 <p>實況 </p> <p>線性 </p> </td> 
   <td colname="col3">參考實現提供 <span class="codeph"> 審核元資料</span> 根據黃金時段廣告部分中提供的資訊連接到用於黃金時段廣告決策的伺服器（以前稱為Auditue）</a> JSON配置檔案</a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 直接廣告分段 </td> 
   <td colname="col2"> 視頻點播 </td> 
   <td colname="col3">必須在輸入JSON檔案中提供廣告URL。 當TVSDK嘗試解析廣告時，它調用直接廣告中斷解析器，並根據JSON配置檔案中提供的直接廣告中斷資訊解析廣告</a>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 自定義廣告標籤 </td> 
   <td colname="col2"> 視頻點播 </td> 
   <td colname="col3">當視頻流既包含主內容和廣告又不包含與廣告位置和時間相關的資訊時，自定義廣告標籤是有用的。 如果以另一種方式獲得廣告定位資訊，例如，通過外部CMS，您可以定義自定義廣告標籤並將其傳遞給播放器時間軸。 <p>要設定播放器以插入廣告，您需要在JSON配置檔案的自定義廣告元資料部分中傳遞廣告元資料</a>在參考實現中有一個支援ad提供方實現。 </p> </td>
  </tr>
 </tbody>
</table>
