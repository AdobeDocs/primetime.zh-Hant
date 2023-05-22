---
title: 許可證伺服器屬性檔案
description: 許可證伺服器屬性檔案
copied-description: true
exl-id: ac105ea6-b5a4-4416-bf17-f619abcf7cd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 許可證伺服器屬性檔案 {#license-server-properties-file}

使用 [!DNL flashaccess-refimpl.properties] 檔案，以配置引用實現的許可證伺服器元件。 至少要配置與傳輸憑據和許可證伺服器憑據相關的屬性。 必須相對於由 `config.resourcesDirectory` 屬性。 此檔案還包含與打包內容相關的幾個屬性：這些屬性僅用於Flash媒體Rights Management伺服器1.x元資料轉換。 如果修改此屬性檔案中的任何值，則需要重新啟動許可證伺服器以使更改生效。

要支援在Adobe訪問中為iOS客戶端生成遠程密鑰傳遞的許可證，必須在中指定密鑰伺服器證書 [!DNL flashaccess-refimpl.properties]。

已在Adobe訪問中添加以下屬性：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">屬性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> 密鑰伺服器的許可證伺服器證書，由Adobe頒發。 當元資料指示需要密鑰伺服器時，此證書用於為iOS設備生成許可證。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">儲存在HSM上的密鑰伺服器Adobe頒發的許可證伺服器證書的別名。 啟用HSM後，請使用此屬性，而不是 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>。 </td> 
  </tr> 
 </tbody> 
</table>
