---
seo-title: 許可證伺服器屬性檔案
title: 許可證伺服器屬性檔案
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 許可證伺服器屬性檔案 {#license-server-properties-file}

使用文 [!DNL flashaccess-refimpl.properties] 件來配置參考實施的許可證伺服器元件。 請務必至少配置與傳輸憑證和許可證伺服器憑證相關的屬性。 必須相對於屬性指定的目錄指定憑據檔案的 `config.resourcesDirectory` 位置。 此檔案也包含數個與封裝內容相關的屬性：這些屬性僅用於Flash Media Rights Management Server 1.x中繼資料轉換。 如果修改了此屬性檔案中的任何值，則需要重新啟動許可證伺服器以使更改生效。

若要支援在Adobe Access中為iOS用戶端產生遠端金鑰傳送的授權，必須在中指定金鑰伺服器憑證 [!DNL flashaccess-refimpl.properties]。

Adobe Access中已新增下列屬性：

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
   <td colname="2" class="- topic/entry "> Adobe核發之Key Server授權伺服器憑證。 當中繼資料指出需要金鑰伺服器時，此憑證會用來產生iOS裝置的授權。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">儲存在HSM上的Key ServerAdobe核發的License Server憑證別名。 啟用HSM時，請使用此屬性，而不 <span class="codeph"> 是HandlerConfiguration.KeyServerCertificate</span>。 </td> 
  </tr> 
 </tbody> 
</table>

