---
title: 組態檔屬性
description: 組態檔屬性
copied-description: true
exl-id: ce4193fa-d217-4134-b08e-715c2cc57c84
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 組態檔屬性 {#configuration-file-properties}

執行「許可證產生器」之前，請指定「許可證產生器」屬性的值。 組態檔指定下列屬性。 屬性名稱包含 *n*， *n* 代表屬性的每個例項都從1開始並遞增的整數。

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
   <td colname="2" class="- topic/entry "> 設定支援的最低使用者端版本。 如果未設定，預設會支援所有版本。 設定此值以控制較舊的使用者端如何回應不支援的授權需求。 指定x (用於Adobe存取x.0)，其中x是主要發行編號。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server憑證(Key Server使用的Adobe核發的License Server憑證)。 只有在中繼資料/原則指出金鑰伺服器是傳遞至iOS裝置的必要專案時，才會使用此憑證。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含簽署授權之License Server認證的PKCS12檔案。 此屬性應該參照包含憑證和私密金鑰的.pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用來保護檔案的密碼，指定者： <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果產生網域繫結授權，則必須指定一個或多個網域CA憑證，以表示此授權簽發者信任的網域授權單位。 如果授權收件者是網域憑證（不是由指定的網域CA所發行），則無法產生授權。 此屬性指定僅包含憑證的.cer檔案（可以接受PEM或DER格式）。 n必須從1開始單調遞增。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">選購的PKCS12檔案，其中包含用於解密中繼資料和原則中CEK的其他授權伺服器認證。 如果內容先前是以License Server憑證封裝，而不是由指定的憑證，則可以設定其他憑證 <span class="codeph"> licensegen.sign.certfile</span>. 此屬性應指 <span class="filepath"> .pfx</span> 包含憑證和私密金鑰的檔案。 n必須從1開始單調遞增。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用來保護檔案的密碼，指定者： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
