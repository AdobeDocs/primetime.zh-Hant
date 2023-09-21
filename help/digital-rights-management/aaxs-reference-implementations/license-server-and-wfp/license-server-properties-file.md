---
title: 授權伺服器屬性檔案
description: 授權伺服器屬性檔案
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 授權伺服器屬性檔案 {#license-server-properties-file}

使用 [!DNL flashaccess-refimpl.properties] 檔案來設定參照實作的License Server元件。 至少請務必設定與傳輸認證和授權伺服器認證相關的屬性。 必須相對於指定的目錄指定認證檔案的位置 `config.resourcesDirectory` 屬性。 此檔案也包含數個與封裝內容相關的屬性：這些屬性僅用於Flash MediaRights Management伺服器1.x中繼資料轉換。 如果您修改此屬性檔案中的任何值，則需要重新啟動許可證伺服器，變更才會生效。

若要在Adobe存取中支援產生傳送至iOS使用者端的遠端金鑰授權，必須在下列位置指定金鑰伺服器憑證： [!DNL flashaccess-refimpl.properties].

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
   <td colname="2" class="- topic/entry "> 金鑰伺服器的授權伺服器憑證，由Adobe簽發。 當中繼資料指出需要金鑰伺服器時，此憑證可用來產生iOS裝置的授權。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Key Server儲存在HSM上的Adobe核發的License Server憑證別名。 啟用HSM時，請改用此屬性，而非 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
