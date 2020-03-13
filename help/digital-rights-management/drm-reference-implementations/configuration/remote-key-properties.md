---
description: 'null'
seo-description: 'null'
seo-title: 遠端金鑰傳送屬性(iOS)
title: 遠端金鑰傳送屬性(iOS)
uuid: 17e1b756-d106-47a7-99ae-641190693870
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 遠端金鑰傳送屬性(iOS){#remote-key-delivery-properties-ios}

若要支援在Adobe Primetime DRM中為iOS用戶端產生遠端金鑰傳送的授權，您必須在檔案中指定金鑰伺服器 `flashaccess-refimpl.properties` 憑證。

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
   <td colname="2" class="- topic/entry "> <p>由Adobe核發之金鑰伺服器授權伺服器憑證。 </p> <p>當中繼資料指出需要金鑰伺服器時，此憑證會產生iOS裝置的授權。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>儲存在HSM上的Key Server Adobe核發之License Server憑證的別名。 </p> <p>啟用HSM時，可以應用此屬性，而不應 <span class="codeph"> 用HandlerConfiguration.KeyServerCertificate屬性</span> 。 </p> </td> 
  </tr> 
 </tbody> 
</table>

