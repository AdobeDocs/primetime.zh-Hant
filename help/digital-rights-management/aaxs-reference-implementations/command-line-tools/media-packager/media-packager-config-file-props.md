---
title: 組態檔屬性
description: 組態檔屬性
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 組態檔屬性 {#configuration-file-properties}

執行「媒體封裝程式」之前，請指定「媒體封裝程式」屬性的值。 組態檔指定下列屬性。 對於包含* n*的屬性名稱， *n* 表示從1開始的整數，並且對於屬性的每個例項都遞增。

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
   <td colname="2" class="- topic/entry "> 指示是否要加密視訊內容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否要加密音訊。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">指示是否加密FLV中的指令碼資料。 <i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> 指令碼資料標籤絕不會加密，即使啟用此選項亦然。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">表示視訊加密等級。 高值會用於加密所有視訊內容，而中值和低值則用於加密包含H.264內容的F4V檔案的視訊內容部分。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大於0，將不會加密檔案開頭指定之內容秒數。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用來加密金鑰的授權伺服器憑證檔案。 此 <span class="codeph"> encrypt.keys.asymmetric.certfile</span> 屬性指定僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此屬性會重複用來建立套用至內容的原則清單。 <span class="codeph"> n</span> 是大於或等於1的整數。 使用者端預設將使用第一個執行個體。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">授權伺服器的傳輸憑證。 此屬性會指定 <span class="filepath"> .cer</span> 僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含封裝程式認證的PKCS12檔案，用於簽署內容。 此 <span class="codeph"> encrypt.sign.certfile</span> 應該指的是 <span class="filepath"> .pfx</span> 包含憑證和私密金鑰的檔案。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用來保護所指定檔案的密碼 <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">設定為封裝的內容發行授權所需的最低伺服器版本。 指定x (Adobe存取x.0)，其中x =主要發行編號。 Adobe存取3.0之前的伺服器不支援此設定。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果原則 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 要求使用與中指定的傳輸憑證不同的伺服器進行網域註冊 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，需要提供網域傳輸憑證。 </p> <p class="- topic/p ">此屬性指定僅包含憑證的檔案（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定授權金鑰。 如果未指定金鑰，則會隨機產生金鑰。 未啟用金鑰輪換時，這是用來加密內容的金鑰。 </p> <p class="- topic/p ">啟用金鑰輪換時，會使用此金鑰來保護輪換金鑰。 金鑰的長度必須是16個位元組，並指定為十六進位值。 十六進位值之間的空白字元為選用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否啟用金鑰輪換。 若設為false （預設），則會停用金鑰輪換，並使用主CEK來加密內容中的所有範例。 </p> <p class="- topic/p ">如果設為true，將啟用金鑰輪換，並且可以使用不同的金鑰來加密內容的部分。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">啟用金鑰輪換時，用來加密內容的輪換金鑰順序。 如果未指定金鑰，則會隨機產生金鑰。 金鑰的長度必須是16個位元組，並指定為十六進位值。 </p> <p class="- topic/p ">十六進位值之間的空白字元為選用。 <i class="+ topic/ph hi-d/i ">n</i> 必須從1開始單調遞增。 指定多個金鑰時，金鑰會依指示的順序循環使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用旋轉金鑰來加密內容範例的間隔（秒）。 </p> <p class="- topic/p ">在內容加密了這段時間後，將使用下一個輪換金鑰。 如果已啟用金鑰輪換且未指定間隔，則會每15分鐘輪換金鑰。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果為true，則沒有可從中取得授權的授權伺服器。 授權必須內嵌或在頻外取得。 若未指定，預設值為false 。 僅支援Adobe Access Professional。 </p> </td> 
  </tr> 
 </tbody> 
</table>
