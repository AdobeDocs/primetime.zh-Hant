---
title: 組態檔屬性
description: 組態檔屬性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 組態檔屬性 {#configuration-file-properties}

在執行「許可證產生器」之前，請指定「許可證產生器」屬性的值。 組態檔指定下列屬性。 針對包含的屬性名稱 *n*， *n* 表示從1開始的整數，並且對於屬性的每個例項都遞增。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 屬性 </th> 
   <th colname="2" class="- topic/entry entry"> 說明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> 設定支援的最低使用者端版本。 如果未設定，預設會支援所有版本。 設定此值以控制較舊的使用者端如何回應不支援的授權需求。 指定x (用於Adobe存取x.0)，其中x為主要發行編號。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 金鑰伺服器憑證(金鑰伺服器使用的Adobe核發的授權伺服器憑證)。 只有在中繼資料/原則指出將金鑰傳遞至iOS裝置需要金鑰伺服器時，才會使用此憑證。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含簽署授權之License Server認證的PKCS12檔案。 此屬性應該參照包含憑證和私密金鑰的.pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用來保護所指定檔案的密碼 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果產生網域繫結授權，則必須指定一或多個網域CA憑證，以指出這個授權簽發者信任的網域授權單位。 如果授權收件者是網域憑證（不是由指定的網域CA發行），則無法產生授權。 此屬性指定僅包含憑證的.cer檔案（可接受PEM或DER格式）。 n必須從1開始單調遞增。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">選用的PKCS12檔案，其中包含用於解密中繼資料和原則中的CEK的其他授權伺服器認證。 如果內容先前是使用License Server憑證封裝，而不是由指定的憑證，則可以設定其他憑證 <span class="codeph"> licensegen.sign.certfile</span>. 此屬性應該參考 <span class="filepath"> .pfx</span> 包含憑證和私密金鑰的檔案。 n必須從1開始單調遞增。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用來保護檔案的密碼，指定者： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
