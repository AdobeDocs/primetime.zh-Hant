---
title: 遠程密鑰傳遞屬性(iOS)
description: 遠程密鑰傳遞屬性(iOS)
copied-description: true
exl-id: 0fe3ed9b-a8ee-43b4-ab3c-8ea2e696503b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 遠程密鑰傳遞屬性(iOS){#remote-key-delivery-properties-ios}

要支援向Adobe PrimetimeDRM中的iOS客戶端生成遠程密鑰傳遞的許可證，必須在 `flashaccess-refimpl.properties` 的子菜單。

以下屬性已添加到Mighine DRM中：

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
   <td colname="2" class="- topic/entry "> <p>由Adobe頒發的密鑰伺服器的許可證伺服器證書。 </p> <p>當元資料指示需要密鑰伺服器時，此證書將為iOS設備生成許可證。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>儲存在HSM上的密鑰伺服器Adobe頒發的許可證伺服器證書的別名。 </p> <p>啟用HSM時，可以應用此屬性，而不是 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> 屬性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
