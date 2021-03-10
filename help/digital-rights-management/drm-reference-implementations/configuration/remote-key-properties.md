---
title: 遠端金鑰傳送屬性(iOS)
description: 遠端金鑰傳送屬性(iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 遠端金鑰傳送屬性(iOS){#remote-key-delivery-properties-ios}

要支援為Adobe PrimetimeDRM的iOS客戶端生成遠程密鑰交付許可，必須在`flashaccess-refimpl.properties`檔案中指定密鑰伺服器證書。

Primetime DRM中已新增下列屬性：

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
   <td colname="2" class="- topic/entry "> <p>由Adobe核發的Key Server授權伺服器憑證。 </p> <p>當中繼資料指出需要金鑰伺服器時，此憑證會產生iOS裝置的授權。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>儲存在HSM上的密鑰伺服器Adobe頒發的許可證伺服器證書的別名。 </p> <p>啟用HSM時，可以應用此屬性，而不應用<span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>屬性。 </p> </td> 
  </tr> 
 </tbody> 
</table>

