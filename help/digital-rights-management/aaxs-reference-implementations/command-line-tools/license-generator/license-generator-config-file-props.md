---
title: 配置檔案屬性
description: 配置檔案屬性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 配置檔案屬性{#configuration-file-properties}

在您執行授權產生器之前，請先為授權產生器屬性指定值。 配置檔案指定以下屬性。 對於包含&#x200B;*n*&#x200B;的屬性名稱，*n*&#x200B;表示從1開始的整數，並且會增加屬性的每個實例。

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
   <td colname="2" class="- topic/entry "> 設定支援的最低用戶端版本。 如果未設定，預設會支援所有版本。 設定此值，以控制較舊的用戶端如何回應他們不支援的授權需求。 指定x(用於Adobe訪問x.0)，其中x是主要發行號。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密鑰伺服器證書(密鑰伺服器使用的Adobe頒發的許可證伺服器證書)。 只有在中繼資料／原則指出必須有金鑰伺服器才能傳送至iOS裝置時，才會使用此憑證。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含用於簽署許可證的許可證伺服器憑據的PKCS12檔案。 此屬性應指包含憑證和私密金鑰的。pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護<span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile.</span>所指定檔案的密碼 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果產生網域系結的授權，則必須指定一或多個網域CA憑證，以指出此授權發行者信任的網域授權機構。 如果授權收件者是網域憑證，而此憑證並非由其中一個指定的網域CA核發，則無法產生授權。 此屬性指定僅包含證書的。cer檔案（PEM或DER格式可接受）。 n必須單調增加，從1開始。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymetic.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可選的PKCS12檔案，包含用於解密元資料和策略中的CEK的附加許可證伺服器憑據。 如果內容先前已封裝為「授權伺服器」憑證，但<span class="codeph"> licensegen.sign.certfile</span>所指定的憑證除外，則可設定其他憑證。 此屬性應引用包含證書和私鑰的<span class="filepath"> .pfx</span>檔案。 n必須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護由以下項目指定的檔案的密碼： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.ansymetic.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

