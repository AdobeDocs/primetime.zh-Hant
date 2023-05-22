---
title: 配置檔案屬性
description: 配置檔案屬性
copied-description: true
exl-id: eec6a53d-d831-4ec4-a90c-8b3e7997f330
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 配置檔案屬性 {#configuration-file-properties}

在運行介質打包器之前，請為介質打包器屬性指定值。 配置檔案指定以下屬性。 對於包含* n*的屬性名， *n* 表示以1開頭的整數，並且為屬性的每個實例遞增。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">屬性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">說明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密視頻內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密音頻。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">指示是否加密FLV中的指令碼資料。 <i class="+ topic/ph hi-d/i ">元資料</i> 和 <i class="+ topic/ph hi-d/i ">在XMP上</i> 即使啟用了此選項，指令碼資料標籤也從不加密。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示視頻加密級別。 高值用於加密所有視頻內容，而中值和低值用於加密包含H.264內容的F4V檔案的部分視頻內容。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.seconds未加密</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，則檔案開頭指定的內容秒數將不會被加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於加密密鑰的許可證伺服器證書檔案。 的 <span class="codeph"> encrypt.keys.asymmetric.cerfile</span> 屬性指定僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性反複用於建立要應用於內容的策略清單。 <span class="codeph"> n</span> 是值為1或更大的整數。 預設情況下，客戶端將使用第一個實例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">許可證伺服器的傳輸證書。 此屬性指定 <span class="filepath"> .cer</span> 僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.cerfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">PKCS12檔案，包含用於簽名內容的打包程式憑據。 的 <span class="codeph"> encrypt.sign.cerfile</span> 應指 <span class="filepath"> .pfx</span> 包含證書和私鑰的檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> 加密.sign.cerpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用於保護由 <span class="codeph"> encrypt.sign.cerfile</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為要打包的內容頒發許可證所需的最低伺服器版本。 指定x(Adobe訪問x.0)，其中x =主發行號。 AdobeAccess 3.0之前的伺服器不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果策略 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 需要向使用與中指定的不同傳輸證書的伺服器註冊域 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，需要提供域傳輸證書。 </p> <p class="- topic/p ">此屬性指定僅包含證書的檔案（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定許可證密鑰。 如果未指定密鑰，則將隨機生成密鑰。 如果未啟用密鑰輪替，則此密鑰用於加密內容。 </p> <p class="- topic/p ">啟用密鑰輪替時，此密鑰用於保護旋轉密鑰。 密鑰的長度必須為16個位元組，並指定為十六進位值。 十六進位值之間的空格是可選的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用密鑰輪替。 如果設定為false（預設），則禁用密鑰輪替，並且主CEK將用於加密內容中的所有示例。 </p> <p class="- topic/p ">如果設定為true，則啟用密鑰輪替，並可以使用不同的密鑰對內容的部分進行加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">啟用密鑰輪替時用於加密內容的旋轉密鑰序列。 如果未指定密鑰，則將隨機生成密鑰。 密鑰的長度必須為16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空格是可選的。 <i class="+ topic/ph hi-d/i ">n</i> 必須單調遞增，從1開始。 指定多個鍵後，按指示的順序循環使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用旋轉密鑰加密內容示例的間隔（秒）。 </p> <p class="- topic/p ">在對內容中的這段時間進行加密後，將使用下一個旋轉密鑰。 如果啟用密鑰輪替且未指定間隔，則每15分鐘輪替一次密鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果為true，則不存在可從中獲取許可證的許可證伺服器。 許可證必須嵌入或帶外獲取。 如果未指定，則預設值為false。 僅在Adobe Access Professional支援。 </p> </td> 
  </tr> 
 </tbody> 
</table>
