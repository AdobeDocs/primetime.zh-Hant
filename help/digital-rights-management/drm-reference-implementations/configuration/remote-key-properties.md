---
title: 遠端金鑰傳遞屬性(iOS)
description: 遠端金鑰傳遞屬性(iOS)
copied-description: true
exl-id: 0fe3ed9b-a8ee-43b4-ab3c-8ea2e696503b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 遠端金鑰傳遞屬性(iOS){#remote-key-delivery-properties-ios}

若要支援在Adobe Primetime DRM中產生將遠端金鑰傳遞至iOS使用者端的授權，您必須在以下位置指定Key Server憑證： `flashaccess-refimpl.properties` 檔案。

Primetime DRM已新增下列屬性：

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
   <td colname="2" class="- topic/entry "> <p>由Adobe所核發的金鑰伺服器授權伺服器憑證。 </p> <p>當中繼資料指出需要金鑰伺服器時，此憑證會產生iOS裝置的授權。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>儲存在HSM上的Key Server之Adobe核發的License Server憑證的別名。 </p> <p>當您啟用HSM時，可以套用此屬性，而不是 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> 屬性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
