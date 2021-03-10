---
title: 許可證伺服器屬性檔案
description: 許可證伺服器屬性檔案
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 許可證伺服器屬性檔案{#license-server-properties-file}

使用[!DNL flashaccess-refimpl.properties]檔案來配置引用實施的許可證伺服器元件。 請務必至少配置與傳輸憑證和許可證伺服器憑證相關的屬性。 必須相對於`config.resourcesDirectory`屬性指定的目錄指定憑據檔案的位置。 此檔案也包含數個與封裝內容相關的屬性：這些屬性僅用於Flash媒體Rights Management伺服器1.x元資料轉換。 如果修改了此屬性檔案中的任何值，則需要重新啟動許可證伺服器以使更改生效。

要支援在Adobe訪問中為iOS客戶端生成遠程密鑰交付的許可證，必須在[!DNL flashaccess-refimpl.properties]中指定密鑰伺服器證書。

下列屬性已新增至Adobe存取：

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
   <td colname="2" class="- topic/entry "> 密鑰伺服器的許可證伺服器證書，由Adobe頒發。 當中繼資料指出需要金鑰伺服器時，此憑證會用來產生iOS裝置的授權。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">儲存在HSM上的密鑰伺服器Adobe頒發的許可證伺服器證書的別名。 啟用HSM時，請使用此屬性，而不是<span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>。 </td> 
  </tr> 
 </tbody> 
</table>

