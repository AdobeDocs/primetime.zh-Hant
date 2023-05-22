---
title: 配置檔案屬性
description: 配置檔案屬性
copied-description: true
exl-id: ce4193fa-d217-4134-b08e-715c2cc57c84
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 配置檔案屬性 {#configuration-file-properties}

運行許可證生成器之前，請為許可證生成器屬性指定值。 配置檔案指定以下屬性。 對於包含的屬性名 *n*。 *n* 表示以1開頭的整數，並且為屬性的每個實例遞增。

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
   <td colname="2" class="- topic/entry "> 設定支援的最低客戶端版本。 如果未設定，則預設情況下支援所有版本。 設定此值，以控制較舊的客戶端如何響應他們不支援的許可證要求。 指定x(用於Adobe訪問x.0)，其中x是主發行號。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密鑰伺服器證書(密鑰伺服器使用的Adobe頒發的許可證伺服器證書)。 僅當元資料/策略指示密鑰伺服器需要密鑰伺服器才能傳遞到iOS設備時，才使用此證書。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含用於簽名許可證的許可證伺服器憑據的PKCS12檔案。 此屬性應引用包含證書和私鑰的.pfx檔案。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.cerpass</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護由 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果生成域綁定的許可證，則必須指定一個或多個域CA證書以指示此許可證頒發者信任的域授權。 如果許可證接收者是域證書，而該證書不是由指定的域CA之一頒發的，則無法生成許可證。 此屬性指定僅包含證書的.cer檔案（PEM或DER格式可接受）。 n必須單調增加，從1開始。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可選PKCS12檔案，包含用於解密元資料和策略中的CEK的其他許可證伺服器憑據。 如果內容以前與許可證伺服器證書打包，而不是由指定的許可證伺服器證書打包，則可以配置其他憑據 <span class="codeph"> licensegen.sign.cerfile</span>。 此屬性應引用 <span class="filepath"> .pfx</span> 包含證書和私鑰的檔案。 n必須單調增加，從1開始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用於保護由以下人員指定的檔案的密碼： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
